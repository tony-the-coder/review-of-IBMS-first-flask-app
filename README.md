# Simple Flask App

This Flask application demonstrates various API endpoints for interacting with a sample dataset of people.

## Setup

1.  **Install Flask:**

    ```bash
    pip install Flask
    ```

2.  **Run the app:**

    ```bash
    python app.py
    ```

## API Endpoints and cURL Examples

The following cURL commands demonstrate how to interact with the API endpoints, following the logical flow of the script:

**1. Basic Routes:**

*   **Get the home page:**

    ```bash
    curl [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
    ```

    This returns a simple "hello world" message.

*   **Get a 204 No Content response:**

    ```bash
    curl -X GET -i -w '\n' localhost:5000/no_content
    ```

    This demonstrates an endpoint returning a 204 No Content response with a JSON message.

*   **Get a 200 OK response:**

    ```bash
    curl -X GET -i -w '\n' localhost:5000/exp
    ```

    This demonstrates an endpoint returning a 200 OK response with a JSON message.

**2. Data-Related Routes:**

*   **Get data count:**

    ```bash
    curl -X GET -i -w '\n' "localhost:5000/count"
    ```

    This returns the number of people in the `data` list.

*   **Get data information:**

    ```bash
    curl -X GET -i -w '\n' localhost:5000/data
    ```

    This returns a message indicating the length of the `data` list or an error if the data is empty or not found.

**3. Person-Related Routes:**

*   **Find a person by UUID:**

    ```bash
    curl -X GET -i localhost:5000/person/66c09925-589a-43b6-9a5d-d1601cf53287
    ```

    This retrieves a person's information by their UUID.

*   **Find a person by an invalid UUID:**

    ```bash
    curl -X GET -i localhost:5000/person/not-a-valid-uuid
    ```

    This returns a 404 Not Found error as the UUID is invalid.

*   **Delete a person by UUID:**

    ```bash
    curl -X DELETE -i localhost:5000/person/66c09925-589a-43b6-9a5d-d1601cf53287
    ```

    This deletes a person from the `data` list based on their UUID.

*   **Get updated data count after deletion:**

    ```bash
    curl -X GET -i -w '\n' "localhost:5000/count"
    ```

    This shows the updated count after deleting a person.

*   **Delete a person with an invalid UUID:**

    ```bash
    curl -X DELETE -i localhost:5000/person/not-a-valid-uuid
    curl -X DELETE -i localhost:5000/person/11111111-589a-43b6-9a5d-d1601cf51111
    ```

    These demonstrate attempts to delete a person with invalid UUIDs, resulting in a 404 Not Found error.

*   **Create a new person:**

    ```bash
    curl -X POST -i -w '\n' \
     --url http://localhost:5000/person \
     --header 'Content-Type: application/json' \
     --data '{
         "id": "4e1e61b4-8a27-11ed-a1eb-0242ac120002",
         "first_name": "John",
         "last_name": "Horne",
         "graduation_year": 2001,
         "address": "1 hill drive",
         "city": "Atlanta",
         "zip": "30339",
         "country": "United States",
         "avatar": "[http://dummyimage.com/139x100.png/cc0000/ffffff](http://dummyimage.com/139x100.png/cc0000/ffffff)"
    }'
    ```

    This creates a new person entry in the `data` list.

*   **Create a person with an empty body:**

    ```bash
    curl -X POST -i -w '\n' \
     --url http://localhost:5000/person \
     --header 'Content-Type: application/json' \
     --data '{}'
    ```

    This attempts to create a person with missing data, resulting in a 400 Bad Request error.

*   **Create a person with an invalid route:**

    ```bash
    curl -X POST -i -w '\n' http://localhost:5000/notvalid
    ```

    This attempts to create a person using an invalid route, demonstrating error handling.

**4. Search Route:**

*   **Search for a person by name:**

    ```bash
    curl -X GET -i -w '\n' "localhost:5000/find_person?q=Abdel"
    ```

    This searches for a person by their first name.

*   **Search with a missing query parameter:**

    ```bash
    curl -X GET -i -w '\n' "localhost:5000/find_person"
    ```

    This demonstrates a search with a missing 'q' parameter, resulting in a 422 Unprocessable Entity error.

*   **Search for a non-existent person:**

    ```bash
    curl -X GET -i -w '\n' "localhost:5000/find_person?q=qwerty"
    ```

    This searches for a person who doesn't exist, returning a 404 Not Found error.

## Additional Notes

*   This app is for demonstration purposes only.
*   Feel free to modify and experiment with the code.
*   Consider adding more features or routes to enhance the app's functionality.
