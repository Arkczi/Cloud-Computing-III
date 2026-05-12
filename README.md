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
2. Przejdź do usługi **CloudFormation** i stwórz nowy stos (Stack), wgrywając plik `AWS_ZADANIE.yaml`.
3. Po zakończeniu instalacji przejdź pod adres URL podany w zakładce **Outputs**.
4. Wykonaj migrację przy użyciu wtyczki all-in-one-wp-migration-6.7 dołączonej w repozytorium (ta wersja omija limit 2kb na backup) po zainstalowaniu wtyczki wgraj plik kopiazapasowasklepu.wpress

## 🛠️ Testy HA (Wysokiej Dostępności)
Infrastruktura została przetestowana pod kątem awarii:
1. Po ręcznym zakończeniu (Terminate) jednej instancji EC2, Load Balancer automatycznie przekierował ruch na drugą maszynę.
2. Auto Scaling Group automatycznie uruchomił nową instancję w miejsce usuniętej.
3. Dzięki zamontowaniu EFS, wszystkie pliki multimedialne pozostały dostępne na obu instancjach.
