"""
Emotion Detection Server

Orchestrates web routing, requests emotion analysis from the
EmotionDetection package, and formats the presentation response.
"""

from flask import Flask, render_template, request
from EmotionDetection import emotion_detector

app = Flask("Emotion Detector")

@app.route("/")
def render_index_page():
    """Renders the main application index page."""
    return render_template("index.html")

@app.route("/emotionDetector")
def detect_emotion():
    """
    Receives text via query parameter, runs emotion detection,
    and returns a formatted string response for the frontend.
    """
    text_to_analyze = request.args.get('textToAnalyze')
    response = emotion_detector(text_to_analyze)

    # Edge Case Handling: Blank input or invalid response
    if response['dominant_emotion'] is None:
        return "Invalid text! Please try again!"

    # Presentation formatting matching the UI contract
    formatted_output = (
        f"For the given statement, the system response is "
        f"'anger': {response['anger']}, "
        f"'disgust': {response['disgust']}, "
        f"'fear': {response['fear']}, "
        f"'joy': {response['joy']} and "
        f"'sadness': {response['sadness']}. "
        f"The dominant emotion is {response['dominant_emotion']}."
    )

    return formatted_output

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)