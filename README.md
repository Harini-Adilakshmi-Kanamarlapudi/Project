# Project
//AI chatbot
from flask import Flask, request, jsonify

app = Flask(__name__)

# Sample intents and responses
intents = {
    "exam_date": "Your next exam is scheduled for September 10, 2025.",
    "cgpa_help": "To improve your CGPA, focus on high-credit subjects and use NPTEL for concept clarity.",
    "resource_request": "You can refer to NPTEL or YouTube for high-quality video lectures on Python.",
    "default": "I'm sorry, I didn't understand that. Can you rephrase?"
}

# Simple keyword-based intent recognition
def recognize_intent(message):
    message = message.lower()
    if "exam" in message:
        return "exam_date"
    elif "cgpa" in message or "grade" in message:
        return "cgpa_help"
    elif "tutorial" in message or "notes" in message or "resource" in message:
        return "resource_request"
    else:
        return "default"

@app.route("/chat", methods=["POST"])
def chat():
    user_input = request.json.get("message")
    intent = recognize_intent(user_input)
    response = intents[intent]
    return jsonify({"response": response})

if __name__ == "__main__":
    app.run(debug=True)
