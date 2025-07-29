# Flag Quiz Game

This is a simple web-based flag quiz game built with Node.js, Express, EJS, and PostgreSQL. The game fetches flag data from a PostgreSQL database, displays a random flag, and allows the user to guess the country name.

## Features

* **Random Flag Display:** Presents a random flag from the database for each question.

* **User Input:** Allows users to type in their guesses for the country name.

* **Score Tracking:** Keeps track of the total correct answers.

* **Feedback:** Provides immediate feedback on whether the answer was correct or incorrect.

## Technologies Used

* **Node.js:** JavaScript runtime environment.

* **Express.js:** Web application framework for Node.js.

* **EJS (Embedded JavaScript):** Templating engine for generating HTML with JavaScript.

* **PostgreSQL:** Relational database for storing flag data.

* **`pg`:** Node.js client for PostgreSQL.

* **`body-parser`:** Middleware to parse incoming request bodies.

## Setup and Installation

### Prerequisites

* Node.js installed on your machine.

* PostgreSQL installed and running.

### Database Setup

1.  **Create a PostgreSQL Database:**
    Create a database named `world` (or any name you prefer, but remember to update `index.js`).

    ```
    CREATE DATABASE world;
    ```

2.  **Create a `flags` Table:**
    Connect to your `world` database and create a table named `flags` with `id`, `name`, and `flag` columns.

    ```
    CREATE TABLE flags (
        id SERIAL PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        flag VARCHAR(255) NOT NULL
    );
    ```

3.  **Import Flag Data:**
    You can import data from a CSV file like `flags.csv` into your `flags` table. Make sure the CSV file has `id`, `name`, and `flag` columns in that order.

    Example `flags.csv` structure:

    ```
    id,name,flag
    1,Afghanistan,🇦🇫
    2,Aland Islands,🇦🇽
    ...
    ```

    You can use a command like `\copy` in `psql` or a GUI tool to import the data:

    ```
    \copy flags(id, name, flag) FROM 'path/to/your/flags.csv' WITH (FORMAT CSV, HEADER);
    ```

    **Note:** Adjust the `id` column in your CSV if it starts from 1 and your table uses `SERIAL` for auto-incrementing IDs. You might need to remove the `id` column from the `\copy` command and let PostgreSQL generate it, or ensure your CSV IDs match the table's sequence.

### Application Setup

1.  **Clone the repository (or create the project structure):**

    ```
    # If you have a git repository
    git clone <repository-url>
    cd <repository-name>

    # If you are creating from scratch, create these files:
    # index.js, package.json, (public/style.css), (views/index.ejs)
    ```

2.  **Install Dependencies:**
    Navigate to the project directory and install the required Node.js packages:

    ```
    npm install
    ```

3.  **Configure Database Connection:**
    Open `index.js` (or `solution.js` if you are using the solution file) and update the PostgreSQL connection details in the `db` object:

    ```javascript
    const db = new pg.Client({
      user: "postgres", // Your PostgreSQL username
      host: "localhost",
      database: "world", // Your database name
      password: "YOUR_POSTGRES_PASSWORD", // Your PostgreSQL password
      port: 5432,
    });
    ```

    **Important:** Replace `"YOUR_POSTGRES_PASSWORD"` with your actual PostgreSQL password.

### Running the Application

1.  **Start the Server:**

    ```
    node index.js
    ```

    (Or `node solution.js` if you are using the solution file)

2.  **Access the Game:**
    Open your web browser and go to:

    ```
    http://localhost:3000
    ```

## Project Structure

* `index.js`: The main server file, handling routes, database queries, and game logic.

* `package.json`: Defines project metadata and lists Node.js dependencies.

* `package-lock.json`: Records the exact versions of dependencies.

* `views/index.ejs`: The EJS template for rendering the game's user interface.

* `public/style.css`: (Optional, but recommended) CSS file for styling the game.

* `flags.csv`: (Provided separately) CSV file containing flag data.

## How to Play

1.  The game will display a flag.

2.  Enter the name of the country corresponding to the flag in the input field.

3.  Click "Submit Answer" to check your guess.

4.  The game will tell you if your answer was correct or incorrect and update your score.

5.  A new flag will be displayed for the next question.

