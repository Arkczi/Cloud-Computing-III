# Sklep E-commerce High-Availability na AWS

Projekt zaliczeniowy . Architektura wysokiej dostępności (HA) oparta na WordPress + WooCommerce.

## 🏗️ Architektura
Projekt wykorzystuje model infrastruktury jako kodu (IaC) i składa się z:
* **VPC:** Sieć z podziałem na podsieci publiczne i prywatne.
* **Auto Scaling Group:** Automatyczne utrzymywanie 2 instancji EC2 w różnych strefach dostępności.
* **Application Load Balancer (ALB):** Rozdzielanie ruchu i monitorowanie stanu maszyn (Health Checks).
* **Amazon RDS (MySQL):** Zewnętrzna baza danych dla WordPressa.
* **Amazon EFS:** Współdzielony system plików dla folderu `/wp-content` (zapewnia synchronizację zdjęć i wtyczek między serwerami).

## 🚀 Instrukcja uruchomienia
1. Zaloguj się do konsoli AWS.
2. Przejdź do usługi **CloudFormation** i stwórz nowy stos (Stack), wgrywając plik `infrastructure.yaml`.
3. Po zakończeniu instalacji przejdź pod adres URL podany w zakładce **Outputs**.
4. (Opcjonalnie) Wykonaj migrację przy użyciu wtyczki All-in-One WP Migration, korzystając z pliku w folderze `/backup`.

## 🛠️ Testy HA (Wysokiej Dostępności)
Infrastruktura została przetestowana pod kątem awarii:
1. Po ręcznym zakończeniu (Terminate) jednej instancji EC2, Load Balancer automatycznie przekierował ruch na drugą maszynę.
2. Auto Scaling Group automatycznie uruchomił nową instancję w miejsce usuniętej.
3. Dzięki zamontowaniu EFS, wszystkie pliki multimedialne pozostały dostępne na obu instancjach.

## Instalacja
1. Pobierz plik yaml. Wejdź w AWS na CloudFormation -> stack i utwóz nowego stacka
2. Pobierz plik kopiazapasowasklepiku i 
