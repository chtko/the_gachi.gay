import requests
from io import BytesIO

def upload_file(url, file_data):
    files = {'file': file_data}
    response = requests.post(url, files=files)
    return response.json()

def main():
    upload_url = "https://gachi.gay/api/upload"

    while True:
        # Замени 'https://example.com/your_photo.jpg' на ссылку на нужное фото или видео
        file_url = input("Введите URL фото или видео (для завершения программы введите 1): ")

        # Проверяем, если пользователь ввел 1, завершаем программу
        if file_url.strip() == '1':
            print("Программа завершена по вашему запросу.")
            break

        try:
            # Получаем содержимое файла по URL
            response = requests.get(file_url, timeout=5)

            # Проверяем успешность запроса
            response.raise_for_status()
        except requests.exceptions.RequestException as e:
            print(f"Ошибка при получении файла: {e}")
            continue

        file_data = BytesIO(response.content)

        # Загружаем файл
        response_json = upload_file(upload_url, file_data)

        # Проверяем успешность загрузки
        if response_json.get('id'):
            file_id = response_json['id']
            uploaded_url = f"https://gachi.gay/{file_id}"
            print(f"Файл успешно загружен. URL: {uploaded_url}")
        else:
            print("Ошибка при загрузке файла.")

if __name__ == "__main__":
    main()
