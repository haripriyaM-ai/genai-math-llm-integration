## EXP-1: Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the Area of Circle, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).
<br><br>
### PROBLEM STATEMENT:
The task is to integrate a mathematical calculation (Area of a Circle) into a Chat Completion system using the function-calling capability of a Large Language Model (LLM). The goal is to let the model recognize when a mathematical operation is required, call a Python function to compute the result, and return the output in a structured JSON format.
<br><br>
### DESIGN STEPS:

#### STEP 1: Define a Python function calculate_circlearea(radius) to compute the area of a circle.

#### STEP 2: Describe the function (name, parameters, and purpose) in a format that the LLM can understand.

#### STEP 3: Pass a user query like “What’s the area of a circle with radius 5?” to the ChatCompletion API along with the function definition.

### STEP 4: Let the model return the function call with arguments, then parse these arguments in Python.

### STEP 5: Execute the function with the parsed input and return the final result.
<br>

### PROGRAM:

```python
 import os
 import openai
 from dotenv import load_dotenv, find_dotenv
 _ = load_dotenv(find_dotenv()) # read local .env file
 openai.api_key = os.environ['OPENAI_API_KEY']
```

```python
 import json
 # Example dummy function hard coded to return the Area of Circle
 # In production, this could be your backend API or an external API
 def calculate_circlearea(radius): #function takes radius input
 """Calculate the Area of Circle"""
 area = 3.14159 * radius * radius # calculates area
 result = {
 
 "radius": radius, #packs result into dictionary
 "area": area,
    }
 return json.dumps(result) #returns result as JSON String
```

```python
 # define a function
 functions = [
    {
 "name": "calculate_circlearea",
 "description": "Calculate the Area of Circle",
 "parameters": {
 "type": "object",
 "properties": {
 "radius": {
 "type": "number",
 "description": "The radius of the circle in units",
                }
            },
 "required": ["radius"],
        }
    }
 ]
```

```python
messages = [
    {
 "role": "user",
 "content": "What's the area of circle with radius 5"
   
```

```python
import openai

```

```python
# Call the ChatCompletion endpoint
 response = openai.ChatCompletion.create(
 model="gpt-3.5-turbo",
 messages=messages,
 functions=functions
 )
```

```python
print(response)
```

```python
response_message = response["choices"][0]["message"]
```

```python
response_message
```

```python
response_message["content"]
```
```python
response_message["function_call"]
```

```python
json.loads(response_message["function_call"]["arguments"])
```

```python
args = json.loads(response_message["function_call"]["arguments"])
```

```python
calculate_circlearea(**args)
```

<br>

### OUTPUT:
<img src="https://github.com/user-attachments/assets/e885bc5c-341b-4b8c-a3f2-e4f94c50d341" width="500" />
<br><br>
<img src="https://github.com/user-attachments/assets/91307b95-ba42-4669-b25f-8eeb910c9ae7" width="500" />
<br><br>
<img src="https://github.com/user-attachments/assets/8a53b651-95f9-4378-9490-eed6c0de6853" width="500" />
<br><br>
<img src="https://github.com/user-attachments/assets/a9c4be98-1de5-4c99-b446-16794fa4d8d0" width="500" />
<br><br>
<img src="https://github.com/user-attachments/assets/5f16fe95-ddfa-4bde-a3c0-cd823d166d27" width="500" />
<br><br>


### RESULT:
The integration of the circle area calculation function with the LLM-based chat completion system was successfully implemented.
