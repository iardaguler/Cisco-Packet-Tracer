# Enterprise Network Topology: Inter-VLAN Routing & Centralized DHCP

<img width="1912" height="1130" alt="image" src="https://github.com/user-attachments/assets/872cf0c0-596b-4180-bf33-f901702287a1" />
<hr>
<br>
Bu proje, ölçeklenebilir bir kurumsal ağ mimarisini simüle etmek amacıyla Cisco Packet Tracer üzerinde tasarlanmıştır. Projenin temel odağı, farklı VLAN'lar arasındaki trafiği yönetmek (Inter-VLAN Routing) ve merkezi bir ağdan dinamik IP dağıtımı sağlamaktır.

🚀 Projenin Amacı
Bu çalışmada, coğrafi veya departman bazlı ayrılmış uç birimlerin (Laptoplar), merkezi bir sunucu bloğuyla (DNS, DHCP, WEB) güvenli ve verimli bir şekilde haberleşmesi amaçlanmıştır.

🛠 Teknik Özellikler ve Yapılandırma
1. Layer 2: VLAN Segmentasyonu
Ağ, mantıksal olarak 4 farklı kullanıcı VLAN'ına bölünmüştür:

Sol Kanat: VLAN 10 & VLAN 20

Sağ Kanat: VLAN 30 & VLAN 40

Amaç: Yayın trafiğini (broadcast domain) kısıtlamak ve ağ güvenliğini artırmak.

2. Layer 3: Router-on-a-Stick (ROAS)
Üstteki ana router (Gateway), switchler üzerinden gelen etiketli (tagged) trafiği sonlandırmak için Subinterface mimarisini kullanır.

Her VLAN için ayrı bir Default Gateway tanımlanmıştır (192.168.x.1).

3. Dinamik Yönlendirme: OSPF (Open Shortest Path First)
Routerlar arası haberleşme ve uzak ağların öğrenilmesi için OSPF 100 protokolü tercih edilmiştir.

Area 0 (Backbone): Tüm ağlar tek bir alan üzerinde toplanmış, hızlı yakınsama (convergence) ve ölçeklenebilirlik sağlanmıştır.

4. Merkezi DHCP ve DHCP Relay Agent
IP yönetimi kolaylığı için sunucu bloğunda merkezi bir DHCP Server konumlandırılmıştır.

IP Helper-Address: Routerlar üzerinde yapılandırılan Relay Agent komutları sayesinde, broadcast olan DHCP Discover paketleri unicast'e çevrilerek merkezi sunucuya başarıyla ulaştırılmaktadır.

5. Sunucu Bloğu (Server Farm)
Ağın alt kısmında yer alan izole bölgede kritik servisler çalışmaktadır:

DNS Server (10.10.10.1): İsim çözümleme.

DHCP Server (10.10.10.2): Dinamik IP ataması.

WEB Server (10.10.10.3): HTTP servis sağlayıcı.
