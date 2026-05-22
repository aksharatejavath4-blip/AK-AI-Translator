# AK-AI-Translator

import streamlit as st
from deep_translator import GoogleTranslator

# Configure the Web Page Layout
st.set_page_config(page_title="CodeAlpha - Language Translator", page_icon="🌐", layout="centered")

# Language Data Mapping
LANGUAGES = {
    "English": "en", "Spanish": "es", "French": "fr", "German": "de", 
    "Hindi": "hi", "Mandarin (Chinese)": "zh-CN", "Arabic": "ar", 
    "Japanese": "ja", "Russian": "ru", "Portuguese": "pt"
}

# Web UI Header Elements
st.title("🌐 AI Language Translation Tool")
st.caption("CodeAlpha Artificial Intelligence Internship Task")
st.markdown("---")

# Responsive Selection Dropdowns
col1, col2 = st.columns(2)
with col1:
    src_lang = st.selectbox("Select Source Language", list(LANGUAGES.keys()), index=0)
with col2:
    dest_lang = st.selectbox("Select Target Language", list(LANGUAGES.keys()), index=1)

# Main Text Input Box
text_to_translate = st.text_area("Enter your text below:", height=150, placeholder="Type sentence here...")

# Translation Button and Execution Logic
if st.button("Translate Text", type="primary", use_container_width=True):
    if text_to_translate.strip():
        try:
            src_code = LANGUAGES[src_lang]
            dest_code = LANGUAGES[dest_lang]
            
            # Request translation from API backend
            translated = GoogleTranslator(source=src_code, target=dest_code).translate(text_to_translate)
            
            # Output container
            st.markdown("### Translated Output:")
            st.success(translated)
            
        except Exception as e:
            st.error(f"An error occurred: {str(e)}")
    else:
        st.warning("Please enter some text before clicking translate!")


