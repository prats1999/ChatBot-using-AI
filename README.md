# ChatBot-using-AI
#Developed a chatbot using AI and NLP techniques

import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer
import random

nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')

conversation_topics = {
    'greeting': ['hi', 'hello', 'hey', 'good morning', 'good afternoon', 'good evening'],
    'weather': ['weather', 'forecast', 'temperature'],
    'farewell': ['bye', 'goodbye', 'see you later']
}

responses = {
    'greeting': ['Hello!', 'Hi there!', 'Hey!'],
    'weather': ['The weather is nice today.', 'It\'s sunny outside.', 'Expect some rain later.'],
    'farewell': ['Goodbye!', 'See you later!', 'Take care!']
}
def preprocess_input(user_input):
   
    tokens = word_tokenize(user_input.lower())
    
    stop_words = set(stopwords.words('english'))
    filtered_tokens = [word for word in tokens if word not in stop_words]
   
    lemmatizer = WordNetLemmatizer()
    lemmatized_tokens = [lemmatizer.lemmatize(word) for word in filtered_tokens]
    return lemmatized_tokens

def get_intent(tokens):
    for word in tokens:
        for intent, keywords in conversation_topics.items():
            if word in keywords:
                return intent
    return None

def generate_response(intent):
    if intent:
        return random.choice(responses[intent])
    else:
        return "I'm not sure how to respond to that."

def chat():
    print("Chatbot: Hi there! How can I help you today?")
    while True:
        user_input = input("You: ")
        if user_input.lower() == 'exit':
            print("Chatbot: Goodbye! Have a great day!")
            break
        preprocessed_input = preprocess_input(user_input)
        intent = get_intent(preprocessed_input)
        response = generate_response(intent)
        print("Chatbot:", response)

if __name__ == "__main__":
    chat()

