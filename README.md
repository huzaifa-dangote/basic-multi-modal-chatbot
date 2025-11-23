# Multi-Modal AI Chatbot for Car Rental Company

A multi-modal AI chatbot built for Exclusive Car Rentals (https://www.ecr.ng) that helps customers find the best vehicle for their needs and guides them through the booking process. The chatbot features text chat, voice responses, and vehicle image generation.

## Features

- **Intelligent Vehicle Recommendations**: AI-powered assistant that helps customers find the perfect vehicle for their rental needs
- **Multi-Modal Interactions**: 
  - Text-based chat interface
  - Voice responses using text-to-speech
  - Vehicle image generation using DALL-E 3
- **Real-Time Pricing**: Queries vehicle pricing database for accurate rental costs
- **Service Type Support**: Handles multiple rental service types:
  - Airport pickup
  - Hourly rate
  - Full day (8 hours)
  - Full 24-hour rental
  - Border states round trip
- **User-Friendly Interface**: Built with Gradio for an intuitive web-based chat experience

## Prerequisites

- Python 3.12 or higher
- OpenAI API key
- SQLite databases (`vehicle.db` and `vehicle_prices.db`)

## Installation

1. **Clone the repository** (if applicable) or navigate to the project directory:
   ```bash
   cd basic-multi-modal-chatbot
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install required packages**:
   ```bash
   pip install python-dotenv openai gradio Pillow
   ```

   Or create a `requirements.txt` file with:
   ```
   python-dotenv
   openai
   gradio
   Pillow
   ```
   Then install with:
   ```bash
   pip install -r requirements.txt
   ```

## Setup

### 1. Environment Variables

Create a `.env` file in the project root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

Replace `your_openai_api_key_here` with your actual OpenAI API key.

### 2. Database Setup

The application requires two SQLite databases:

- **`vehicle.db`**: Contains vehicle information
- **`vehicle_prices.db`**: Contains pricing information with the following schema:
  - Table: `vehicle_prices`
  - Columns: `vehicle_id`, `service_type`, `price`

Ensure both database files are present in the project root directory. The `vehicle_prices.db` should have entries matching the vehicle IDs and service types defined in the code.

### 3. Available Vehicles

The chatbot supports the following vehicles:
- Toyota Coaster
- Mercedes G-Wagon
- Toyota Hiace 2018
- Toyota Land Cruiser 2020
- Mercedes Sprinter
- Lexus GX 460
- Toyota Hilux
- Lexus LX 470
- Toyota Camry
- Toyota Prado
- Hyundai H1
- Toyota Land Cruiser
- Toyota Hiace

## Usage

1. **Open the Jupyter Notebook**:
   ```bash
   jupyter notebook app.ipynb
   ```

2. **Run all cells** in order (or use "Run All" from the Cell menu)

3. **Access the chatbot interface**: The Gradio interface will automatically open in your browser at `http://127.0.0.1:7870`

4. **Interact with the chatbot**:
   - Type your message in the text box
   - The chatbot will respond with:
     - Text response in the chat window
     - Audio response (automatically plays)
     - Vehicle image (if a vehicle is mentioned)

## How It Works

1. **User Input**: User types a message in the chat interface
2. **AI Processing**: The chatbot uses GPT-4.1-mini to understand the request
3. **Function Calling**: If pricing information is needed, the chatbot calls the `get_vehicle_price` function
4. **Database Query**: The function queries `vehicle_prices.db` for the requested vehicle and service type
5. **Multi-Modal Response**: The chatbot generates:
   - A text response
   - A voice response using GPT-4o-mini TTS (Coral voice)
   - A vehicle image using DALL-E 3 (if a vehicle is mentioned)

## Project Structure

```
basic-multi-modal-chatbot/
├── app.ipynb              # Main Jupyter notebook with chatbot implementation
├── vehicle.db             # SQLite database with vehicle information
├── vehicle_prices.db      # SQLite database with pricing information
├── README.md              # This file
└── .env                   # Environment variables (create this file)
```

## Technologies Used

- **OpenAI API**: 
  - GPT-4.1-mini for chat completions
  - GPT-4o-mini TTS for text-to-speech
  - DALL-E 3 for image generation
- **Gradio**: Web interface framework
- **SQLite**: Database for vehicle and pricing information
- **Python Libraries**:
  - `python-dotenv`: Environment variable management
  - `Pillow`: Image processing

## API Models Used

- **Chat Model**: `gpt-4.1-mini`
- **Image Generation**: `dall-e-3` (1024x1024)
- **Text-to-Speech**: `gpt-4o-mini-tts` (Coral voice)

## Service Types

The chatbot supports the following service types:
- `airport_pickup`: Airport pickup service
- `hourly_rate`: Hourly rental
- `full_day_8hr`: 8-hour full day rental
- `full_24hr`: 24-hour rental
- `border_states_roundtrip`: Round trip to border states

## Notes

- The chatbot defaults to `airport_pickup` service type if the user doesn't specify one
- Vehicle images are generated on-demand using DALL-E 3 when a vehicle is mentioned
- All voice responses are automatically played in the interface
- The chatbot is designed to be polite, friendly, and stay within the scope of vehicle rental services

## Troubleshooting

- **API Key Issues**: Ensure your `.env` file is in the project root and contains a valid `OPENAI_API_KEY`
- **Database Errors**: Verify that both `vehicle.db` and `vehicle_prices.db` exist and contain the required data
- **Import Errors**: Make sure all required packages are installed in your virtual environment
- **Port Already in Use**: If port 7870 is in use, Gradio will automatically select another port
