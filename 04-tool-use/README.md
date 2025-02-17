# Tool Use Design Pattern  

## Introduction

In this lesson, we're looking to answer the following questions:

- What is the tool use design pattern?
- What are the use cases it can be applied to?
- What are the elements/building blocks needed to implement the design pattern?
- What are the special considerations for using the Tool Use Design Pattern to build trustworthy AI agents?

## Learning Goals

After completing this lesson, you will be able to:

- Define the Tool Use Design Pattern and its purpose.
- Identify use cases where the Tool Use Design Pattern is applicable.
- Understand the key elements needed to implement the design pattern.
- Recognize considerations for ensuring trustworthiness in AI agents using this design pattern.

## What is the Tool Use Design Pattern?

The **Tool Use Design Pattern** focuses on giving LLMs the ability to interact with external tools to achieve specific goals. Tools are code that can be executed by an agent to perform actions. A tool can be a simple function such as a calculator, or an API call to a third-party service such as stock price lookup or weather forecast. In the context of AI agents, tools are designed to be executed by agents in response to **model-generated function calls**.

## What are the use cases it can be applied to?

AI Agents can leverage tools to complete complex tasks, retrieve information, or make decisions. The tool use design pattern is often used in scenarios requiring dynamic interaction with external systems, such as databases, web services, or code interpreters. This ability is useful for a number of different use cases including:

- **Dynamic Information Retrieval:** Agents can query external APIs or databases to fetch up-to-date data (e.g., querying a SQLite database for data analysis, fetching stock prices or weather information).
- **Code Execution and Interpretation:** Agents can execute code or scripts to solve mathematical problems, generate reports, or perform simulations.
- **Workflow Automation:** Automating repetitive or multi-step workflows by integrating tools like task schedulers, email services, or data pipelines.
- **Customer Support:** Agents can interact with CRM systems, ticketing platforms, or knowledge bases to resolve user queries.
- **Content Generation and Editing:** Agents can leverage tools like grammar checkers, text summarizers, or content safety evaluators to assist with content creation tasks.

## What are the elements/building blocks needed to implement the tool use design pattern?

### Function/Tool Calling

Function calling is the primary way we enable Large Language Models (LLMs) to interact with tools. You will often see 'Function' and 'Tool' used interchangeably because 'functions' (blocks of reusable code) are the 'tools' agents use to carry out tasks. In order for a function's code to be invoked, an LLM must compare the users request against the functions description. To do this a schema containing the descriptions of all the available functions is sent to the LLM. The LLM then selects the most appropriate function for the task and returns its name and arguments. The selected function is invoked, it's response is sent back to the LLM, which uses the information to respond to the users request.

For developers to implement function calling for agents, you will need:

1. An LLM model that supports function calling
2. A schema containing function descriptions
3. The code for each function described

Let's use the example of getting the current time in a city to illustrate:

- **Initialize an LLM that supports function calling:**

    Not all models support function calling, so it's important to check that the LLM you are using does. [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/how-to/function-calling){target="_blank"} supports function calling. We can start by initiating the Azure OpenAI client. 

    ```python
    # Initialize the Azure OpenAI client
    client = AzureOpenAI(
        azure_endpoint = os.getenv("AZURE_OPENAI_ENDPOINT"), 
        api_key=os.getenv("AZURE_OPENAI_API_KEY"),  
        api_version="2024-05-01-preview"
    )
    ```

- **Create a Function Schema**:

    Next we will define a JSON schema that contains the function name, description of what the function does, and the names and descriptions of the function parameters.
    We will then take this schema and pass it to the client created above, along with the users request to find the time in San Francisco. Whats important to note is that a **tool call** is what is returned, **not** the final answer to the question. As mentioned earlier, the LLM returns the name of the function it selected for the task, and the arguments that will be passed to it. 

    ```python
    # Function description for the model to read
    tools = [
        {
            "type": "function",
            "function": {
                "name": "get_current_time",
                "description": "Get the current time in a given location",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "location": {
                            "type": "string",
                            "description": "The city name, e.g. San Francisco",
                        },
                    },
                    "required": ["location"],
                },
            }
        }
    ]
    ```
   
    ```python
  
    # Initial user message
    messages = [{"role": "user", "content": "What's the current time in San Francisco"}] 
  
    # First API call: Ask the model to use the function
      response = client.chat.completions.create(
          model=deployment_name,
          messages=messages,
          tools=tools,
          tool_choice="auto",
      )
  
      # Process the model's response
      response_message = response.choices[0].message
      messages.append(response_message)
  
      print("Model's response:")  

      print(response_message)
  
    ```

    ```bash
    Model's response:
    ChatCompletionMessage(content=None, role='assistant', function_call=None, tool_calls=[ChatCompletionMessageToolCall(id='call_pOsKdUlqvdyttYB67MOj434b', function=Function(arguments='{"location":"San Francisco"}', name='get_current_time'), type='function')])
    ```
  
- **The function code required to carry out the task:**

    Now that the LLM has chosen which function needs to be run the code that carries out the task needs to be implemented and executed.
    We can implement the code to get the current time in Python. We will also need to write the code to extract the name and arguments from the response_message to get the final result.

    ```python
      def get_current_time(location):
        """Get the current time for a given location"""
        print(f"get_current_time called with location: {location}")  
        location_lower = location.lower()
        
        for key, timezone in TIMEZONE_DATA.items():
            if key in location_lower:
                print(f"Timezone found for {key}")  
                current_time = datetime.now(ZoneInfo(timezone)).strftime("%I:%M %p")
                return json.dumps({
                    "location": location,
                    "current_time": current_time
                })
      
        print(f"No timezone data found for {location_lower}")  
        return json.dumps({"location": location, "current_time": "unknown"})
    ```

     ```python
     # Handle function calls
      if response_message.tool_calls:
          for tool_call in response_message.tool_calls:
              if tool_call.function.name == "get_current_time":
     
                  function_args = json.loads(tool_call.function.arguments)
     
                  time_response = get_current_time(
                      location=function_args.get("location")
                  )
     
                  messages.append({
                      "tool_call_id": tool_call.id,
                      "role": "tool",
                      "name": "get_current_time",
                      "content": time_response,
                  })
      else:
          print("No tool calls were made by the model.")  
  
      # Second API call: Get the final response from the model
      final_response = client.chat.completions.create(
          model=deployment_name,
          messages=messages,
      )
  
      return final_response.choices[0].message.content
     ```

     ```bash
      get_current_time called with location: San Francisco
      Timezone found for san francisco
      The current time in San Francisco is 09:24 AM.
     ```

Function Calling is at the heart of most, if not all agent tool use design, however implementing it from scratch can sometimes be challenging.
As we learned in [Lesson 2](../02-explore-agentic-frameworks/) agentic frameworks provide us with pre-built building blocks to implement tool use.
 
### Tool Use Examples with Agentic Frameworks

- ### **[Semantic Kernel](https://learn.microsoft.com/azure/ai-services/agents/overview){target="_blank"}**

    Semantic Kernel is an open-source AI framework for .NET, Python, and Java developers working with Large Language Models (LLMs). It simplifies the process of using function calling by automatically describing your functions and their parameters to the model through a process called [serializing](https://learn.microsoft.com/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-python#1-serializing-the-functions){target="_blank"}. It also handles the back-and-forth communication between the model and your code. Another advantage of using an agentic framework like Semantic Kernel, is that it allows you to access pre-built tools like [File Search](https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step4_assistant_tool_file_search.py){target="_blank"} and [Code Interpreter](https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step3_assistant_tool_code_interpreter.py){target="_blank"}.

    The following diagram illustrates the process of function calling with Semantic Kernel:

    ![function calling](./images/functioncalling-diagram.png)


    In Semantic Kernel functions/tools are called [Plugins](https://learn.microsoft.com/semantic-kernel/concepts/plugins/?pivots=programming-language-python){target="_blank"}. We can convert the `get_current_time` function we saw earlier into a plugin by turning it into a class with the function in it. We can also import the `kernel_function` decorator, which takes in the description of the function. When you then create a kernel with the GetCurrentTimePlugin, the kernel will automatically serialize the function and its parameters, creating the schema to send to the LLM in the process.

    ```python
    from semantic_kernel.functions import kernel_function

    class GetCurrentTimePlugin:
        async def __init__(self, location):
            self.location = location

        @kernel_function(
            description="Get the current time for a given location"
        )
        def get_current_time(location: str = ""):
            ...

    ```

    ```python 
    from semantic_kernel import Kernel

    # Create the kernel
    kernel = Kernel()

    # Create the plugin
    get_current_time_plugin = GetCurrentTimePlugin(location)

    # Add the plugin to the kernel
    kernel.add_plugin(get_current_time_plugin)
    ```
  
- ### **[Azure AI Agent Service](https://learn.microsoft.com/azure/ai-services/agents/overview){target="_blank"}**

    Azure AI Agent Service is a newer agentic framework that is designed to empower developers to securely build, deploy, and scale high-quality, and extensible AI agents without needing to manage the underlying compute and storage resources. It is particularly useful for enterprise applications since it is a fully managed service with enterprise grade security. 

    When compared to developing with the LLM API directly, Azure AI Agent Service provides some advantages, including:
  - Automatic tool calling – no need to parse a tool call, invoke the tool, and handle the response; all of this is now done server-side
  - Securely managed data – instead of managing your own conversation state, you can rely on threads to store all the information you need
  - Out-of-the-box tools – Tools that you can use to interact with your data sources, such as Bing, Azure AI Search, and Azure Functions.

    The tools available in Azure AI Agent Service can be divided into two categories:

    1. Knowledge Tools:
        - [Grounding with Bing Search](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/bing-grounding?tabs=python&pivots=overview){target="_blank"}
        - [File Search](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/file-search?tabs=python&pivots=overview){target="_blank"}
        - [Azure AI Search](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/azure-ai-search?tabs=azurecli%2Cpython&pivots=overview-azure-ai-search){target="_blank"}

    2. Action Tools:
        - [Function Calling](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/function-calling?tabs=python&pivots=overview){target="_blank"}
        - [Code Interpreter](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/code-interpreter?tabs=python&pivots=overview){target="_blank"}
        - [OpenAI defined tools](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/openapi-spec?tabs=python&pivots=overview){target="_blank"}
        - [Azure Functions](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/azure-functions?pivots=overview){target="_blank"}

    The Agent Service allows us to be able to use these tools together as a `toolset`. It also utilizes `threads` which keep track of the history of messages from a particular conversation.

    Imagine you are a sales agent at a company called Contoso. You want to develop a conversational agent that can answer questions about your sales data.

    The image below illustrates how you could use Azure AI Agent Service to analyze your sales data:

    ![Agentic Service In Action](./images/agent-service-in-action.jpg?WT.mc_id=academic-105485-koreyst)

    To use any of these tools with the service we can create a client and define a tool or toolset. To implement this practically we can use the Python code below. The LLM will be able to look at the toolset and decide whether to use the user created function, `fetch_sales_data_using_sqlite_query`, or the pre-built Code Interpreter depending on the user request.

    ```python 
    import os
    from azure.ai.projects import AIProjectClient
    from azure.identity import DefaultAzureCredential
    from fecth_sales_data_functions import fetch_sales_data_using_sqlite_query # fetch_sales_data_using_sqlite_query function which can be found in a fetch_sales_data_functions.py file.
    from azure.ai.projects.models import ToolSet, FunctionTool, CodeInterpreterTool

    project_client = AIProjectClient.from_connection_string(
        credential=DefaultAzureCredential(),
        conn_str=os.environ["PROJECT_CONNECTION_STRING"],
    )

    # Initialize function calling agent with the fetch_sales_data_using_sqlite_query function and adding it to the toolset
    fetch_data_function = FunctionTool(fetch_sales_data_using_sqlite_query)
    toolset = ToolSet()
    toolset.add(fetch_data_function)

    # Initialize Code Interpreter tool and adding it to the toolset. 
    code_interpreter = code_interpreter = CodeInterpreterTool()
    toolset = ToolSet()
    toolset.add(code_interpreter)

    agent = project_client.agents.create_agent(
        model="gpt-4o-mini", name="my-agent", instructions="You are helpful agent", 
        toolset=toolset
    )
    ```

## What are the special considerations for using the Tool Use Design Pattern to build trustworthy AI agents?

A common concern with SQL dynamically generated by LLMs is security, particularly the risk of SQL injection or malicious actions, such as dropping or tampering with the database. While these concerns are valid, they can be effectively mitigated by properly configuring database access permissions. For most databases this involves configuring the database as read-only. For database services like PostgreSQL or Azure SQL, the app should be assigned a read-only (SELECT) role. R

Running the app in a secure environment further enhances protection. In enterprise scenarios, data is typically extracted and transformed from operational systems into a read-only database or data warehouse with a user-friendly schema. This approach ensures that the data is secure, optimized for performance and accessibility, and that the app has restricted, read-only access.

## Additional Resources

- [Azure AI Agents Service Workshop](https://microsoft.github.io/build-your-first-agent-with-azure-ai-agent-service-workshop/){target="_blank"}
- [Contoso Creative Writer Multi-Agent Workshop](https://github.com/Azure-Samples/contoso-creative-writer/tree/main/docs/workshop){target="_blank"}
- [Semantic Kernel Function Calling Tutorial](https://learn.microsoft.com/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-python#1-serializing-the-functions){target="_blank"}
- [Semantic Kernel Code Interpreter](https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step3_assistant_tool_code_interpreter.py){target="_blank"}
- [Autogen Tools](https://microsoft.github.io/autogen/dev/user-guide/core-user-guide/components/tools.html){target="_blank"}
