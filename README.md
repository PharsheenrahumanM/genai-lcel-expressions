## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:

### DESIGN STEPS:

#### STEP 1:Create a template with at least two input variables

#### STEP 2:Choose a language model (like GPT-4) to process the prompt.

#### STEP 3:Set up a parser to extract structured data.

### PROGRAM:
~~~
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import ResponseSchema
from langchain.schema.output_parser import StrOutputParser

# Define the PromptTemplate
prompt = PromptTemplate(
    template="""
You are a travel assistant. Based on the following inputs, recommend a destination:
- Preferred activity: {activity}
- Budget (in USD): {budget}

Provide a response strictly in JSON format:
{{
    "destination": "<destination>",
    "activity": "<activity>",
    "cost": "<cost>"
}}
""",
    input_variables=["activity", "budget"],
)

# Define the Output Parser
response_schemas = [
    ResponseSchema(name="destination", description="Recommended travel destination"),
    ResponseSchema(name="activity", description="Suggested activity at the destination"),
    ResponseSchema(name="cost", description="Estimated cost in USD for the trip"),
]
output_parser = StrOutputParser()

# Initialize the LLM
llm = ChatOpenAI(model="gpt-4-0613", temperature=0)

# Create the LangChain Expression (LLM Chain)
chain = LLMChain(llm=llm, prompt=prompt, output_parser=output_parser)

# Test the chain with an example
input_data = {"activity": "hiking", "budget": 1000}
result = chain.run(input_data)

# Parse the structured output
parsed_result = output_parser.parse(result)

# Display the result
print("Recommendation:", parsed_result)
~~~

### OUTPUT
![image](https://github.com/user-attachments/assets/1b203351-5ac5-490a-a25c-da291a269e25)



### RESULT:Thus, the program is developed and executed successfully to implement a LangChain Expression Language (LCEL) expression that incorporates at least two input parameters and the three essential components—prompt, model, and output parser—while also demonstrating its functionality through analysis of practical real-world examples.
