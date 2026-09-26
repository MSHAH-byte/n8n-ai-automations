# Project 1 — Daily Weather Email Automation

## Overview

This project is a simple automated weather notification workflow built with **n8n**.

Every day at **6:00 AM**, the workflow retrieves current weather data for **Peshawar, Pakistan** using the **Open-Meteo API** and sends the current temperature and wind speed to an email address through **Gmail**.

The project demonstrates a basic n8n automation pattern:

```text
Schedule Trigger
       ↓
   HTTP Request
       ↓
      Gmail
```

It is the first project in this repository and focuses on learning how n8n connects scheduled triggers, external APIs, and communication services.

## Workflow

### 1. Schedule Trigger

**Node:** `Schedule Trigger`

The workflow is configured to run automatically every day at **6:00 AM**.

### 2. HTTP Request

**Node:** `HTTP Request`

The workflow calls the **Open-Meteo Forecast API** using the coordinates for Peshawar:

* Latitude: `34.0151`
* Longitude: `71.5249`

The request retrieves the following current weather data:

* `temperature_2m` — Current temperature
* `relative_humidity_2m` — Relative humidity
* `weather_code` — Weather condition code
* `wind_speed_10m` — Wind speed

Although all four fields are retrieved from the API, only **`temperature_2m`** and **`wind_speed_10m`** are currently mapped into the Gmail message.

### 3. Gmail

**Node:** `Send a message`

The Gmail node sends a plain-text email containing:

* Current temperature
* Current wind speed

The email subject is:

> Daily Weather

The workflow uses n8n expressions to dynamically extract the values from the Open-Meteo API response:

```text
$json.current.temperature_2m
$json.current.wind_speed_10m
```

The relative humidity and weather code are retrieved by the HTTP Request node but are **not currently included in the email body**.

## Example Flow

```text
6:00 AM
   ↓
Schedule Trigger
   ↓
Open-Meteo API
   ↓
Current Weather Data
   ↓
Extract Temperature & Wind Speed
   ↓
Gmail
   ↓
Daily Weather Email
```

## Technologies Used

* **n8n** — Workflow automation and orchestration
* **Open-Meteo API** — Weather data source
* **Gmail** — Email delivery
* **HTTP Request** — REST API integration
* **n8n Expressions** — Dynamic data mapping

## Project Structure

```text
project-1-weather-email/
├── Project 1 - Daily Weather.json
└── README.md
```

* `Project 1 - Daily Weather.json` — Exported n8n workflow.
* `README.md` — Project documentation.

## Setup

### 1. Install and Start n8n

Start your local n8n instance:

```bash
n8n
```

The n8n editor is available at:

```text
http://localhost:5678
```

### 2. Import the Workflow

Import the following file into your n8n instance:

```text
Project 1 - Daily Weather.json
```

### 3. Configure Gmail

Authenticate a Gmail account using n8n's Gmail OAuth2 credentials.

Update the recipient email address in the **Send a message** node if necessary.

### 4. Activate the Workflow

After configuring the Gmail credentials, activate the workflow.

The Schedule Trigger will execute the workflow automatically at **6:00 AM** each day.

## Testing

The workflow can be tested manually from the n8n editor.

A successful execution should:

1. Trigger the workflow.
2. Send a request to Open-Meteo.
3. Receive the current weather data.
4. Extract the temperature and wind speed.
5. Send the weather information through Gmail.

## Key Takeaways

This project demonstrates the fundamental n8n automation pattern:

**Trigger → External Data → Action**

The workflow shows how n8n can:

* Run tasks on a schedule.
* Connect to an external REST API.
* Process JSON responses.
* Map API data using expressions.
* Send automated emails.
* Connect multiple services without writing a custom backend.

It serves as a simple foundation for the more advanced automation and AI-agent workflows in the other projects in this repository.

## Security

No API key is required for the Open-Meteo request used in this workflow.

Do not commit private credentials, OAuth tokens, passwords, or other secrets to the repository.
