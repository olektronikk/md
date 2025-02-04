### ping test 

### arp test



#### IPBUS 
??? Рамки success

            200002f0 2000011f 00000030 00001234
    Req Data: f0020020 1f010020 30000000 34120000 (write - Adress 30 - data 1234)
    Res Data: f0020020 10010020

            200003f0 2000010f 00000030
    Req Data: f0030020 0f010020 30000000   (read - Adress 30)  
    Res Data: f0030020 00010020 34120000	
            20000100 00001234


    Data: 	  f0040020 00010020 34120000

#### Python code 
??? Отправлнеи success
    Отпавление статусной пачки  полученеи статусного ответа

    ```python
    import socket

    def send_udp_data():
        # IP и порт назначения
        target_ip = "192.168.1.15"
        target_port = 50001  # Укажите порт, который вам нужен

        # Данные для отправки (в формате hex)
        hex_data = "200000f1000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"

        # Преобразуем hex-строку в байты
        data = bytes.fromhex(hex_data)

        # Создаем UDP-сокет
        with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as udp_socket:
            try:
                # Привязываем сокет к локальному адресу и порту 0 (пусть ОС выберет порт автоматически)
                udp_socket.bind(("", 0))
                local_port = udp_socket.getsockname()[1]
                print(f"Сокет привязан к порту {local_port} для отправки/получения данных")

                # Отправляем данные
                udp_socket.sendto(data, (target_ip, target_port))
                print(f"Данные отправлены на {target_ip}:{target_port}")

                # Ожидаем ответ
                udp_socket.settimeout(5)  # Устанавливаем тайм-аут на получение данных
                try:
                    data, addr = udp_socket.recvfrom(1024)  # Получаем данные (макс. 1024 байта)
                    print(f"Получены данные от {addr}: {data.hex()}")

                    # Разбиваем данные на блоки по 8 бит и выводим их в столбец
                    print("Разбивка данных на блоки по 8 бит:")
                    for byte in data:
                        print(f"{byte:08X}")
                except socket.timeout:
                    print("Ответ не был получен в течение установленного времени")
            except Exception as e:
                print(f"Ошибка при отправке/приеме данных: {e}")

                
    if __name__ == "__main__":
        send_udp_data()
    ```