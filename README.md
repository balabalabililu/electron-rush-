# electron-rush-
An interactive chemistry game

import random

# ELECTRON RUSH: Chemistry Game
# Materi: Konfigurasi elektron kulit atom

ELEMENTS = {
    1: ("Hidrogen", "H", [1]),
    2: ("Helium", "He", [2]),
    3: ("Litium", "Li", [2, 1]),
    4: ("Berilium", "Be", [2, 2]),
    5: ("Boron", "B", [2, 3]),
    6: ("Karbon", "C", [2, 4]),
    7: ("Nitrogen", "N", [2, 5]),
    8: ("Oksigen", "O", [2, 6]),
    9: ("Fluorin", "F", [2, 7]),
    10: ("Neon", "Ne", [2, 8]),
    11: ("Natrium", "Na", [2, 8, 1]),
    12: ("Magnesium", "Mg", [2, 8, 2]),
    13: ("Aluminium", "Al", [2, 8, 3]),
    14: ("Silikon", "Si", [2, 8, 4]),
    15: ("Fosfor", "P", [2, 8, 5]),
    16: ("Sulfur", "S", [2, 8, 6]),
    17: ("Klorin", "Cl", [2, 8, 7]),
    18: ("Argon", "Ar", [2, 8, 8]),
    19: ("Kalium", "K", [2, 8, 8, 1]),
    20: ("Kalsium", "Ca", [2, 8, 8, 2]),
}

def config_text(config):
    return ", ".join(map(str, config))

def make_question():
    z = random.randint(1, 20)
    name, symbol, config = ELEMENTS[z]
    mode = random.randint(1, 3)

    if mode == 1:
        question = f"Nomor atom {z} punya konfigurasi elektron..."
        answer = config_text(config)
        explanation = f"{name} ({symbol}), Z={z}"

    elif mode == 2:
        question = (
            f"Konfigurasi elektron {config_text(config)} "
            "adalah unsur apa?"
        )
        answer = name.lower()
        explanation = f"Unsur tersebut adalah {name} ({symbol}), Z={z}"

    else:
        question = (
            f"Unsur {name} ({symbol}) memiliki nomor atom berapa?"
        )
        answer = str(z)
        explanation = f"Nomor atom {name} adalah {z}"

    return question, answer, explanation

def play():
    score = 0
    lives = 3
    total = 10

    print("=" * 38)
    print("       ELECTRON RUSH")
    print("  MISSION: KONFIGURASI ELEKTRON")
    print("=" * 38)
    print("Jawab 10 soal. Kamu punya 3 nyawa!")
    input("\nTekan ENTER untuk mulai...")

    for number in range(1, total + 1):
        if lives <= 0:
            break

        question, answer, explanation = make_question()

        print("\n" + "-" * 38)
        print(f"LEVEL {number} | Skor: {score} | Nyawa: {lives}")
        print(question)

        user_answer = input("Jawabanmu: ").strip().lower()
        normalized = user_answer.replace(" ", "")

        if normalized == answer.replace(" ", ""):
            print("BENAR! +10 poin!")
            score += 10
        else:
            print(f"Belum tepat! Jawaban: {answer}")
            lives -= 1

        print("INFO:", explanation)

    print("\n" + "=" * 38)
    print("         MISI SELESAI!")
    print(f"Skor akhir: {score}/{total * 10}")
    print(f"Sisa nyawa: {lives}")

    if score == 100:
        print("PERFECT! Kamu master konfigurasi elektron!")
    elif score >= 70:
        print("HEBAT! Pengetahuan kimiamu makin kuat!")
    elif score >= 40:
        print("LUMAYAN! Ayo latihan lagi!")
    else:
        print("Jangan menyerah! Coba lagi dan naik level!")

    print("=" * 38)

while True:
    play()
    again = input("\nMain lagi? (y/n): ").strip().lower()
    if again != "y":
        print("Terima kasih sudah bermain!")
        break
