from fastapi import FastAPI, File, UploadFile
from fastapi.responses import Response

app = FastAPI()

@app.get("/")
def home():
    return {"status": "Server is online and ready!"}

@app.post("/voice")
async def handle_voice(file: UploadFile = File(...)):
    audio_bytes = await file.read()
    print(f"Отримано аудіо від ESP32. Розмір: {len(audio_bytes)} байт")
    
    # Поки що сервер відправляє отримане аудіо назад (для перевірки зв'язку)
    return Response(content=audio_bytes, media_type="audio/wav")
