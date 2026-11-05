"""
Emotion Detection Server Application.

This module sets up a Flask web application that serves the frontend
and interfaces with the EmotionDetection package to provide real-time
emotion scoring for user-submitted text.
"""

from flask import Flask, render_template, request
from EmotionDetection import emotion_detector

app = Flask("Emotion Detector")


@app.route("/")
def render_index_page():
    """Render the application index page."""
    return render_template("index.html")


@app.route("/emotionDetector")
def detect_emotion():
    """
    Handle emotion detection requests.

    Extracts text to analyze from the query parameter, runs emotion
    detection, and returns a formatted response or an error message.
    """
    text_to_analyze = request.args.get("textToAnalyze")
    response = emotion_detector(text_to_analyze)

    if response["dominant_emotion"] is None:
        return "Invalid text! Please try again!"

    anger = response["anger"]
    disgust = response["disgust"]
    fear = response["fear"]
    joy = response["joy"]
    sadness = response["sadness"]
    dominant = response["dominant_emotion"]

    return (
        f"For the given statement, the system response is "
        f"'anger': {anger}, 'disgust': {disgust}, 'fear': {fear}, "
        f"'joy': {joy} and 'sadness': {sadness}. "
        f"The dominant emotion is {dominant}."
    )


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
