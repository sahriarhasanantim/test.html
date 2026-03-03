import streamlit as st
import google.generativeai as genai
from PIL import Image

# --- API KEY SETUP ---
GOOGLE_API_KEY = "AIzaSyDRg62_K1Na7elDVFhVroay9C-Mk-I5rqs"
genai.configure(api_key=GOOGLE_API_KEY)

# Model setup (Gemini 1.5 Flash image o bujhte pare)
model = genai.GenerativeModel('gemini-1.5-flash')

# --- WEBSITE UI ---
st.set_page_config(page_title="Gemini Vision AI", page_icon="📸")

st.title("📸 Gemini Vision AI Assistant")
st.write("Ekhon apni chobi upload koreo amar sathe kotha bolte parben!")

# Sidebar-e chobi upload korar option
with st.sidebar:
    st.header("Upload Section")
    uploaded_file = st.file_uploader("Ekti chobi select korun...", type=["jpg", "jpeg", "png"])
    if uploaded_file:
        image = Image.open(uploaded_file)
        st.image(image, caption="Apnar Upload kora chobi", use_column_width=True)

# Chat History initialization
if "messages" not in st.session_state:
    st.session_state.messages = []

# Purono messages display
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# User Input
if prompt := st.chat_input("Chobi-ti niye kichu jiggesh korun..."):
    st.session_state.messages.append({"role": "user", "content": prompt})
    with st.chat_message("user"):
        st.markdown(prompt)

    with st.chat_message("assistant"):
        message_placeholder = st.empty()
        
        try:
            # Jodi chobi upload kora thake, tobe chobi + text eksathe pathano hobe
            if uploaded_file:
                response = model.generate_content([prompt, image])
            else:
                response = model.generate_content(prompt)
                
            full_response = response.text
            message_placeholder.markdown(full_response)
        except Exception as e:
            full_response = "Dukkhito, chobi-ti analyze korte somossa hochhe."
            st.error(f"Error: {e}")

    st.session_state.messages.append({"role": "assistant", "content": full_response})
