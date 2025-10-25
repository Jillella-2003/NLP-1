# Word Cloud Generator using NLP
# Install dependencies: pip install wordcloud nltk matplotlib

import nltk
from nltk.corpus import stopwords
from wordcloud import WordCloud
import matplotlib.pyplot as plt

# Download NLTK stopwords (first time only)
nltk.download('stopwords')

# Function to clean text
def preprocess_text(text):
    # Convert to lowercase
    text = text.lower()
    # Tokenize and remove stopwords
    stop_words = set(stopwords.words('english'))
    words = text.split()
    words = [word for word in words if word.isalpha() and word not in stop_words]
    clean_text = ' '.join(words)
    return clean_text

# Function to generate word cloud
def generate_wordcloud(text, title="Word Cloud"):
    clean_text = preprocess_text(text)
    wordcloud = WordCloud(width=800, height=400, background_color='white', colormap='viridis',
                          max_words=200, contour_width=3, contour_color='steelblue').generate(clean_text)

    # Display the word cloud
    plt.figure(figsize=(15, 7))
    plt.imshow(wordcloud, interpolation='bilinear')
    plt.axis('off')
    plt.title(title, fontsize=20)
    plt.show()

# Main program
if __name__ == "__main__":
    print("=== Word Cloud Generator using NLP ===")
    choice = input("Do you want to enter (1) text manually or (2) read from a file? Enter 1 or 2: ")

    if choice == '1':
        text_input = input("Enter your text: ")
    elif choice == '2':
        file_path = input("Enter file path (e.g., sample.txt): ")
        with open(file_path, 'r', encoding='utf-8') as file:
            text_input = file.read()
    else:
        print("Invalid choice. Exiting...")
        exit()

    generate_wordcloud(text_input)
