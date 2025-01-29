**Automatyzacja konfiguracji maszyn wirtualnych z Vagrant & VirtualBox**


📌 Opis projektu
Projekt zawiera konfigurację Vagranta umożliwiającą automatyczne tworzenie dwóch maszyn wirtualnych:

Python Development (python-dev) – środowisko do programowania w Pythonie, zawierające m.in. Pythona 3, JupyterLab, PyCharm, Docker oraz PostgreSQL.
C++ Development (cpp-dev) – środowisko do programowania w C++, zawierające m.in. GCC, Clang, CMake, GDB oraz VS Code.
Maszyny działają w tej samej sieci prywatnej, co pozwala na łatwą komunikację między nimi.


🚀 Jak uruchomić projekt?
1. Zainstaluj wymagane narzędzia:
  - Vagrant
  - VirtualBox
2. Sklonuj repozytorium
  git clone *https://github.com/Bysiaa/dev-ev/*
  cd twoje-repozytorium
3. Uruchom maszyny wirtualne
  vagrant up
4. Po zakończeniu konfiguracji zaloguj się do jednej z maszyn:
  - Python Dev: vagrant ssh python-dev
  - C++ Dev: vagrant ssh cpp-dev


✅ Konfiguracja maszyn
1. Python Development (python-dev)
  - Python 3, pip, venv
  - JupyterLab
  - Docker
  - PostgreSQL
  - PyCharm
2. C++ Development (cpp-dev)
  - GCC, Clang, CMake
  - GDB, Valgrind
  - VS Code


📂 Struktura repozytorium
/repozytorium
│── Vagrantfile             # Konfiguracja maszyn wirtualnych
│── python_projects/        # Folder na projekty Pythonowe (synchronizowany)
│── cpp_projects/           # Folder na projekty C++ (synchronizowany)
│── README.md               # Ten plik!


💡 Przydatne komendy
Sprawdzenie statusu maszyn: vagrant status
Restart maszyny: vagrant reload
Zatrzymanie maszyn: vagrant halt
Usunięcie maszyn: vagrant destroy
