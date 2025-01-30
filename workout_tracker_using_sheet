import requests
import os
from datetime import datetime
# from dotenv import load_dotenv
import os
apiKey = os.getenv("NUTRITIONIX_APPKEY")
NUTRITIONIX_APPID = os.getenv("NUTRITIONIX_APPID")
sheet_id = os.getenv("sheet_id")
sheet_username = os.getenv("sheet_username")
NUTRITIONIX_END_POINT = "https://trackapi.nutritionix.com/v2/natural/exercise"
SHEETY_URL = f"https://api.sheety.co/{sheet_id}/{sheet_username}/workouts"
import base64

encoded_credentials= os.getenv("SHEETY_BASIC_CREDENTIALS")
 #base64.b64encode(credentials.encode()).decode()


headers_for_sheety = {
    "Authorization": f"Basic {encoded_credentials}"
}

today = datetime.now().strftime("%Y/%m/%d")

headers = {
    "x-app-id":NUTRITIONIX_APPID,
    "x-app-key":apiKey
}
print(SHEETY_URL)
data ={
"query":input("enter the exercise way -> ")
}

response = requests.post(url=NUTRITIONIX_END_POINT, json=data,headers=headers)

exercise_data = response.json()  # which is an array and need to traverse it and then post for each


# print(exercise_data)
for exercise_d in exercise_data["exercises"]:
    # print(exercise_d)
    workout = {
        "workout":{
            "date": today,
            "time": datetime.now().strftime("%H:%M:%S"),
            "exercise": exercise_d["name"],
            "duration": exercise_d["duration_min"],
            "calories": exercise_d["nf_calories"]
        }
    }

    response = requests.post(url=SHEETY_URL,json=workout,headers=headers_for_sheety)
    print(response.text)
