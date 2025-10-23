import socket

# Test edilecek hedef IP adresi
target_ip = "10.10.10.1" # Kendi bilgisayarınız (localhost)

print(f"{target_ip} üzerindeki portlar taranıyor...")

try:
    # Yaygın olarak kullanılan bazı portları deneyelim
    for port in range(1, 1025):  
        # Bir soket nesnesi oluşturuyoruz
        # AF_INET: IPv4 adres ailesini belirtir
        # SOCK_STREAM: TCP bağlantısını belirtir
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        
        # Zaman aşımı süresi belirliyoruz, böylece kapalı portlarda çok beklemeyiz
        socket.setdefaulttimeout(0.5)
        
        # Porta bağlanmayı deniyoruz
        result = sock.connect_ex((target_ip, port))
        
        # connect_ex() fonksiyonu başarılı olursa 0 döner
        if result == 0:
            print(f"Port :{port} [Açık]")
            
        # Soketi kapatıyoruz
        sock.close()

except KeyboardInterrupt:
    print("\nTarama kullanıcı tarafından iptal edildi.")
except socket.gaierror:
    print("\nHostname çözümlenemedi. IP adresini kontrol edin.")
except socket.error:
    print("\nSunucuya bağlanılamadı.")

print("\nTarama tamamlandı.")
