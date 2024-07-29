# NASCAR Motorsport API

The **NASCAR Motorsport API** provides comprehensive access to data from the world of NASCAR, including real-time updates, driver statistics, race information, and historical records. This API is ideal for developers, sports analysts, and NASCAR enthusiasts, delivering detailed insights into various NASCAR events and drivers. This API can be found here: [NASCAR Motorsport API](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/nascar-motorsport-api)

## Key Features

- **Live Race Data**: Access real-time updates during NASCAR races, including lap times, positions, and race events.
- **Driver Statistics**: Retrieve detailed profiles and statistics for NASCAR drivers, including race results and championship standings.
- **Race Information**: Get information on NASCAR races, including schedules, locations, and race results.
- **Team Information**: Access data on NASCAR teams, including team rosters and performance metrics.
- **Historical Data**: Access past race results and driver statistics for comprehensive analysis and historical comparisons.

## Getting Started

1. **Sign Up**: Create an account on RapidAPI.
2. **Subscribe**: Choose a subscription plan that fits your needs.
3. **API Key**: Obtain your unique API key to start making requests.
4. **Documentation**: For detailed usage instructions, visit the [NASCAR Motorsport API Documentation](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/nascar-motorsport-api).


### Endpoint

#### Retrieve Race Results

- **URL:** `/results`
- **Method:** `GET`
- **Description:** Fetches the race results for the specified year and series. Utilizes caching to enhance performance and reduce server load.

### Query Parameters

| Parameter | Type   | Description                                 | Required | Default Value |
|-----------|--------|---------------------------------------------|----------|---------------|
| `year`    | `int`  | The year of the race results to retrieve    | Yes      | 2024          |
| `series`  | `int`  | The series of the race results to retrieve  | Yes      | 1             |

### Series Values

The `series` parameter can have the following values:

| Value | Series Name               |
|-------|----------------------------|
| 1     | NASCAR Cup Series          |
| 2     | NASCAR Xfinity Series      |
| 3     | NASCAR Truck Series        |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing the race results for the specified year and series.
  - **Example:**
    ```json
    {
      "results": [
        {
          "race_name": "Daytona 500",
          "date": "2024-02-18",
          "winner": "Driver A",
          "team": "Team A"
        },
        {
          "race_name": "Coca-Cola 600",
          "date": "2024-05-26",
          "winner": "Driver B",
          "team": "Team B"
        }
      ]
    }
    ```

- **Error Responses:**
  - **Code:** 400 Bad Request
    - **Content:** JSON object with an error message indicating that the year or series is missing or invalid.
    - **Example:**
      ```json
      {
        "error": "Please enter the year"
      }
      ```
      ```json
      {
        "error": "Invalid series value. The accepted values are: 1, 2, 3. Read the documentation for more information"
      }
      ```
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store the race results data to enhance performance and reduce the load on the server.
- If the data for the requested year and series is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/results?year=2024&series=1"
```

### Endpoint

#### Retrieve Race Results for a Driver

- **URL:** `/race-results`
- **Method:** `GET`
- **Description:** Fetches the race results for a specific driver and year. Utilizes caching to enhance performance and reduce server load.

### Query Parameters

| Parameter | Type   | Description                                     | Required | Default Value |
|-----------|--------|-------------------------------------------------|----------|---------------|
| `driverId`| `string`| The ID of the driver whose race results to retrieve | Yes      | '810'         |
| `year`    | `int`  | The year of the race results to retrieve        | Yes      | 2024          |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing the race results for the specified driver and year.
  - **Example:**
    ```json
    {
      "race_results": [
        {
          "race_name": "Daytona 500",
          "date": "2024-02-18",
          "position": 3,
          "team": "Team A"
        },
        {
          "race_name": "Coca-Cola 600",
          "date": "2024-05-26",
          "position": 5,
          "team": "Team B"
        }
      ]
    }
    ```

- **Error Responses:**
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store the race results data for 1 hour (3600 seconds) to improve performance and reduce the load on the server.
- If the data for the requested driver and year is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/race-results?driverId=810&year=2024"
```
#### Retrieve Race Report

- **URL:** `/race-report`
- **Method:** `GET`
- **Description:** Fetches the race report for a specific race identified by `raceId`. Utilizes caching to enhance performance and minimize server load.

### Query Parameters

| Parameter | Type   | Description                                     | Required | Default Value |
|-----------|--------|-------------------------------------------------|----------|---------------|
| `raceId`  | `string`| The ID of the race for which to retrieve the report | Yes      | '202302054248'|

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing the detailed race report for the specified `raceId`.
  - **Example:**
    ```json
    {
      "race_report": {
        "race_id": "202302054248",
        "race_name": "Daytona 500",
        "date": "2024-02-18",
        "winner": "Driver A",
        "winning_team": "Team A",
        "laps": [
          { "lap_number": 1, "position": 1, "driver": "Driver A" },
          { "lap_number": 2, "position": 1, "driver": "Driver A" },
          // More laps
        ]
      }
    }
    ```

- **Error Responses:**
  - **Code:** 400 Bad Request
    - **Content:** JSON object with an error message indicating that the `raceId` is missing.
    - **Example:**
      ```json
      {
        "error": "Please provide the raceId"
      }
      ```
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store the race report data to enhance performance and reduce the load on the server.
- If the data for the requested `raceId` is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/race-report?raceId=202302054248"
```

#### Retrieve Scoreboard Data

- **URL:** `/scoreboard`
- **Method:** `GET`
- **Description:** Fetches the scoreboard data for the specified year, with optional filters for month and day. Utilizes caching to improve performance and reduce server load.

### Query Parameters

| Parameter | Type   | Description                                       | Required | Default Value |
|-----------|--------|---------------------------------------------------|----------|---------------|
| `year`    | `int`  | The year of the scoreboard data to retrieve       | Yes      | 2023          |
| `month`   | `int`  | The month of the scoreboard data to retrieve (optional) | No       | null          |
| `day`     | `int`  | The day of the scoreboard data to retrieve (optional)   | No       | null          |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing the scoreboard data for the specified year, month, and day.
  - **Example:**
    ```json
    {
      "scoreboard": [
        {
          "team": "Team A",
          "score": 85,
          "opponent": "Team B",
          "date": "2023-05-14"
        },
        {
          "team": "Team C",
          "score": 92,
          "opponent": "Team D",
          "date": "2023-05-14"
        }
      ]
    }
    ```

- **Error Responses:**
  - **Code:** 400 Bad Request
    - **Content:** JSON object with an error message indicating that the year is missing.
    - **Example:**
      ```json
      {
        "error": "Please enter the year"
      }
      ```
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store the scoreboard data to enhance performance and reduce the load on the server.
- If the data for the requested year, month, and day is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/scoreboard?year=2023&month=5&day=14"
```
#### Retrieve Current Scoreboard

- **URL:** `/current-scoreboard`
- **Method:** `GET`
- **Description:** Fetches the most recent scoreboard data. Utilizes caching to enhance performance and reduce server load.

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing the latest scoreboard data.
  - **Example:**
    ```json
    {
      "scoreboard": [
        {
          "team": "Team A",
          "score": 85,
          "opponent": "Team B",
          "date": "2024-07-29"
        },
        {
          "team": "Team C",
          "score": 92,
          "opponent": "Team D",
          "date": "2024-07-29"
        }
      ]
    }
    ```

- **Error Responses:**
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store the current scoreboard data for 1 hour (3600 seconds) to improve performance and reduce server load.
- If the data for the current scoreboard is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/current-scoreboard"
```

#### Retrieve Nascar News

- **URL:** `/news`
- **Method:** `GET`
- **Description:** Fetches the latest Nascar news articles with support for pagination. Utilizes caching to improve performance and reduce server load.

### Query Parameters

| Parameter | Type   | Description                                   | Required | Default Value |
|-----------|--------|-----------------------------------------------|----------|---------------|
| `page`    | `int`  | The page number of news articles to retrieve | Yes      | 1             |
| `perPage` | `int`  | The number of news articles per page          | Yes      | 15            |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing a list of news articles.
  - **Example:**
    ```json
    {
      "news": [
        {
          "title": "Nascar Announces New Regulations for 2025",
          "date": "2024-07-29",
          "summary": "Nascar has unveiled new regulations that will come into effect in 2025, aimed at improving safety and competition."
        },
        {
          "title": "Driver X Wins Major Race",
          "date": "2024-07-28",
          "summary": "Driver X has secured a stunning victory in the latest Nascar race, cementing their position as a top contender for the championship."
        }
      ],
      "pagination": {
        "page": 1,
        "perPage": 15,
        "totalPages": 10
      }
    }
    ```

- **Error Responses:**
  - **Code:** 400 Bad Request
    - **Content:** JSON object with an error message indicating that required parameters are missing.
    - **Example:**
      ```json
      {
        "message": "Please provide the page parameter value!"
      }
      ```
      ```json
      {
        "message": "Please provide the perPage parameter value!"
      }
      ```
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store news articles data for 1 hour (3600 seconds) to improve performance and reduce the load on the server.
- If the data for the requested page and perPage parameters is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/news?page=1&perPage=15"
```

#### Retrieve Athlete Information

- **URL:** `/athlete-info`
- **Method:** `GET`
- **Description:** Fetches detailed information about a specific athlete. Utilizes caching to enhance performance and minimize server load.

### Query Parameters

| Parameter   | Type   | Description                             | Required | Default Value |
|-------------|--------|-----------------------------------------|----------|---------------|
| `athleteId` | `string`| The ID of the athlete whose information to retrieve | Yes      | '4495'        |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing detailed information about the specified athlete.
  - **Example:**
    ```json
    {
      "athlete_info": {
        "id": "4495",
        "name": "John Doe",
        "team": "Team A",
        "position": "Driver",
        "stats": {
          "total_races": 150,
          "wins": 30,
          "top_5_finishes": 50
        }
      }
    }
    ```

- **Error Responses:**
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store athlete information data for 1 hour (3600 seconds) to improve performance and reduce the load on the server.
- If the data for the requested `athleteId` is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/athlete-info?athleteId=4495"
```

#### Retrieve Driver Statistics

- **URL:** `/stats`
- **Method:** `GET`
- **Description:** Fetches detailed statistics for a specified driver. Utilizes caching to enhance performance and minimize server load.

### Query Parameters

| Parameter   | Type   | Description                             | Required | Default Value |
|-------------|--------|-----------------------------------------|----------|---------------|
| `driverId`  | `string` | The ID of the driver whose statistics to retrieve | Yes      | '4495'        |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing detailed statistics for the specified driver.
  - **Example:**
    ```json
    {
      "driver_stats": {
        "id": "4495",
        "name": "John Doe",
        "total_races": 150,
        "average_position": 5.2,
        "total_wins": 30,
        "top_5_finishes": 50
      }
    }
    ```

- **Error Responses:**
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store driver statistics data for 1 hour (3600 seconds) to improve performance and reduce server load.
- If the data for the requested `driverId` is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/stats?driverId=4495"
```

#### Retrieve Driver Photos

- **URL:** `/photos`
- **Method:** `GET`
- **Description:** Fetches photos of a specific driver with support for pagination. Utilizes caching to improve performance and reduce server load.

### Query Parameters

| Parameter   | Type   | Description                                 | Required | Default Value |
|-------------|--------|---------------------------------------------|----------|---------------|
| `driverId`  | `string` | The ID of the driver whose photos to retrieve | Yes      | '4495'        |
| `page`      | `string` | The page number of photos to retrieve        | No       | '1'           |

### Responses

- **Success Response:**
  - **Code:** 200 OK
  - **Content:** JSON object containing a list of photos for the specified driver.
  - **Example:**
    ```json
    {
      "photos": [
        {
          "url": "https://example.com/photos/driver-4495-1.jpg",
          "caption": "Driver 4495 at the podium"
        },
        {
          "url": "https://example.com/photos/driver-4495-2.jpg",
          "caption": "Driver 4495 during a race"
        }
      ],
      "pagination": {
        "page": 1,
        "totalPages": 5
      }
    }
    ```

- **Error Responses:**
  - **Code:** 500 Internal Server Error
    - **Content:** JSON object with an error message indicating a server issue.
    - **Example:**
      ```json
      {
        "error": "Something went wrong: Please try again later or change the parameters!"
      }
      ```

### Caching

- The API uses caching to store driver photos data for 1 hour (3600 seconds) to improve performance and reduce the load on the server.
- If the data for the requested `driverId` and `page` parameters is already cached, the API will serve the response from the cache.

### Example Request

```sh
curl -X GET "https://api.example.com/photos?driverId=4495&page=1"
```

## Commonly Asked Questions

### 1. What kind of data can I access through the NASCAR Motorsport API?
You can access live race data, driver statistics, race information, team information, and historical data.

### 2. How do I authenticate my API requests?
You need to include your API key in the headers of your requests as specified in the API documentation.

### 3. Are there usage limits for the API?
Yes, usage limits depend on the subscription plan you select. Check the RapidAPI dashboard for details.

### 4. Can I filter data by specific races, drivers, or teams?
Yes, the API allows filtering to retrieve data for specific races, drivers, or teams.

### 5. Is historical data available for past NASCAR events?
Yes, the NASCAR Motorsport API includes historical data for past events, allowing for detailed analysis and comparisons.

### 6. How frequently is the data updated?
The data is updated in real-time during live races and periodically for historical data and schedules.

### 7. Can I access data for different NASCAR series?
Yes, the API provides data for various NASCAR series, covering a wide range of events and drivers.

### 8. What formats does the API support for data responses?
The API supports data responses in JSON format, making it easy to integrate into various applications.

### 9. Are there specific endpoints for different types of data (e.g., race results, driver stats)?
Yes, the API includes specific endpoints for various types of data, such as race results, driver statistics, and team information.

### 10. How can I stay updated on changes to the API?
You can stay informed about updates and changes by checking the API documentation and RapidAPI dashboard regularly.

For more information and to start using the NASCAR Motorsport API, visit [NASCAR Motorsport API on RapidAPI](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/nascar-motorsport-api).
