import streamlit as st
import google.generativeai as genai
import random
from dotenv import load_dotenv
import os

# Load environment variables
load_dotenv()
api_key = os.getenv("GOOGLE_API_KEY")
genai.configure(api_key=api_key)

# Generation config
generation_config = {
    "temperature": 0.75,
    "top_p": 0.95,
    "top_k": 64,
    "max_output_tokens": 8192,
    "response_mime_type": "text/plain",
}

model = genai.GenerativeModel(
    model_name="gemini-2.5-flash",
    generation_config=generation_config
)

# CSS Styling
st.markdown(
    """
    <style>
    /* Background */
    .stApp {
        background-color: #2e2e2e; /* dark gray background */
        font-family: 'Arial', sans-serif;
        color: #ffffff; /* default text color white */
    }

    /* Main heading */
    .main-heading {
        color: #ffffff;
        font-size: 36px;
        font-weight: bold;
        margin-bottom: 10px;
    }

    /* Subheading */
    .sub-heading {
        color: #dddddd;
        font-size: 20px;
        margin-bottom: 20px;
    }

    /* Joke box */
    .joke-box {
        background-color: #555555; /* medium gray */
        padding: 15px;
        border-radius: 10px;
        margin-bottom: 20px;
        font-style: italic;
        color: #ffcc00; /* yellow text for jokes */
    }

    /* Recipe output */
    .recipe-output {
        background-color: #444444; /* slightly darker gray */
        padding: 20px;
        border-radius: 10px;
        border: 1px solid #666666;
        margin-top: 10px;
        color: #ffffff;
    }

    /* Button styling */
    .stButton>button {
        background-color: #e74c3c;
        color: white;
        font-size: 18px;
        padding: 10px 20px;
        border-radius: 8px;
    }

    /* Input fields */
    div.stTextInput > div > input,
    div.stNumberInput > div > input {
        background-color: #666666 !important;  /* dark gray input background */
        color: #ffffff !important;             /* white text */
        border: 1px solid #888888 !important;  /* border for visibility */
    }

    div.stTextInput > label,
    div.stNumberInput > label {
        color: #ffffff !important;  /* label text white */
    }

    </style>
    """, unsafe_allow_html=True
)


# Page heading
st.markdown('<div class="main-heading">RecepieMaster: AI-Powered Blog Generation</div>', unsafe_allow_html=True)
st.markdown('<div class="sub-heading">🤖 Hello! I’m recepieMaster, your friendly robot. Let’s create a fantastic recipe together!</div>', unsafe_allow_html=True)

# Function to generate a joke
def get_joke():
    jokes = [
        "Why don't programmers like nature? It has too many bugs.",
        "Why do Java developers wear glasses? Because they don't see sharp.",
        "Why was the JavaScript developer sad? Because he didn't know how to 'null' his feelings.",
        "Why do programmers prefer dark mode? Because light attracts bugs!",
        "Why do Python programmers prefer using snake_case? Because it's easier to read!",
        "How many programmers does it take to change a light bulb? None, that's a hardware problem.",
        "Why did the developer go broke? Because he used up all his cache.",
        "Why do programmers always mix up Christmas and Halloween? Because Oct 31 == Dec 25.",
        "Why did the programmer get kicked out of the beach? Because he kept using the 'C' language!",
        "Why was the computer cold? It left its Windows open."
    ]
    return random.choice(jokes)

# Recipe generation function
def recipe_generation(user_input, word_count):
    """
    Function to generate a recipe based on user input and word count.
    """

    st.markdown(f'<div class="joke-box">While I work on creating your recipe, here\'s a little joke to keep you entertained:<br><b>{get_joke()}</b></div>', unsafe_allow_html=True)

    try:
        chat_session = model.start_chat(
            history=[
                {
                    "role": "user",
                    "parts": [
                        f"Write a recipe about {user_input} in approximately {word_count} words."
                    ],
                }
            ]
        )

        response = chat_session.send_message(user_input)

        st.success("✅ Your recipe is ready!")
        st.markdown(f'<div class="recipe-output">{response.text}</div>', unsafe_allow_html=True)

    except Exception as e:
        st.error(f"Error generating recipe: {e}")

# Input fields
user_input = st.text_input("Enter recipe topic")
word_count = st.number_input(
    "Enter word count",
    min_value=100,
    max_value=1000,
    value=300
)

if st.button("Generate Recipe"):
    if user_input:
        recipe_generation(user_input, word_count)
    else:
        st.warning("Please enter a recipe topic!")
