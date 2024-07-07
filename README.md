Q1. Explain GET and POST methods.
GET and POST are two of the most commonly used HTTP methods for sending requests to a server.

GET Method:

Purpose: Retrieve data from a server.
Characteristics:
Data is appended to the URL as query parameters.
Generally used for fetching data without modifying it.
Parameters are visible in the URL, so it is not suitable for sensitive data.
Has size limitations on the amount of data that can be sent.
Example:

python
Copy code
@app.route('/data', methods=['GET'])
def get_data():
    name = request.args.get('name')
    return f'Hello, {name}!'
POST Method:

Purpose: Send data to the server to create or update a resource.
Characteristics:
Data is included in the body of the request.
Generally used for actions that change the server's state, like creating a new record or updating existing data.
Data is not visible in the URL, so it is suitable for sensitive data.
No size limitations on the amount of data that can be sent.
Example:

python
Copy code
@app.route('/data', methods=['POST'])
def post_data():
    data = request.form['data']
    return f'Data received: {data}'
Q2. Why is request used in Flask?
In Flask, the request object is used to access incoming request data. This object allows you to get information about the request such as form data, query parameters, headers, and more. It is essential for handling data submitted by the client to the server.

Common uses:

Form Data: request.form to access form fields.
Query Parameters: request.args to access URL query parameters.
JSON Data: request.json to access JSON payloads.
Headers: request.headers to access HTTP headers.
Q3. Why is redirect() used in Flask?
The redirect() function in Flask is used to redirect the user to a different endpoint. It generates a response that instructs the client to make a new request to the provided URL.

Common uses:

After Form Submission: Redirecting to a different page after form submission to avoid resubmission on page refresh.
URL Shortening: Redirecting from a short URL to a longer target URL.
Authorization: Redirecting unauthenticated users to a login page.
Q4. What are templates in Flask? Why is the render_template() function used?
Templates in Flask are files that contain static HTML as well as dynamic placeholders for content that can be rendered with data at runtime. They allow for separation of business logic and presentation layer.

render_template() is used to render a template file with specific context data. It loads the template file and replaces the placeholders with actual data provided as arguments.

Example:

python
Copy code
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html', title='Home', message='Welcome to the homepage!')

if __name__ == '__main__':
    app.run()
In index.html:

html
Copy code
<!doctype html>
<html>
<head>
    <title>{{ title }}</title>
</head>
<body>
    <h1>{{ message }}</h1>
</body>
</html>
Q5. Create a simple API. Use Postman to test it. Attach the screenshot of the output in the Jupyter Notebook.
Simple API Example:

python
Copy code
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/api/data', methods=['GET'])
def get_data():
    data = {
        'name': 'John Doe',
        'age': 30,
        'location': 'New York'
    }
    return jsonify(data)

@app.route('/api/data', methods=['POST'])
def post_data():
    new_data = request.json
    response = {
        'message': 'Data received',
        'data': new_data
    }
    return jsonify(response), 201

if __name__ == '__main__':
    app.run(debug=True)
Testing with Postman:

GET Request:

URL: http://127.0.0.1:5000/api/data
Method: GET
Output: JSON data with name, age, and location.
POST Request:

URL: http://127.0.0.1:5000/api/data
Method: POST
Body (raw JSON):
json
Copy code
{
    "name": "Jane Doe",
    "age": 25,
    "location": "San Francisco"
}
Output: Confirmation message with the sent data.
Screenshots:

Since I can't run the Flask server directly in this notebook, I can't provide real-time screenshots. However, you can follow the steps provided, run the Flask app, and test it with Postman to see the results.

To include the screenshots in your Jupyter Notebook, you can use the following markdown:

markdown
Copy code
### GET Request in Postman
![GET Request](path_to_your_screenshot.png)

### POST Request in Postman
![POST Request](path_to_your_screenshot.png)
