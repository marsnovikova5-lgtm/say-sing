from midiutil import MIDIFile

# Создаем MIDI-файл
midi = MIDIFile(1)  # одна дорожка
track = 0
time = 0
midi.addTrackName(track, time, "Papa Song")
midi.addTempo(track, time, 70)  # медленный темп

# Ноты для аккордов (тональность Am)
chords = {
    "Am": [57, 60, 64],   # A, C, E
    "F": [53, 57, 60],    # F, A, C
    "C": [48, 52, 55],    # C, E, G
    "G": [55, 59, 62],    # G, B, D
}

# Прогрессии аккордов
verse = ["Am", "F", "C", "G"]
chorus = ["F", "C", "G", "Am"]

duration = 4  # длительность одного аккорда (в четвертях)
volume = 90

current_time = 0

# Куплет (2 раза)
for _ in range(2):
    for chord in verse:
        for note in chords[chord]:
            midi.addNote(track, 0, note, current_time, duration, volume)
        current_time += duration

# Припев (2 раза)
for _ in range(2):
    for chord in chorus:
        for note in chords[chord]:
            midi.addNote(track, 0, note, current_time, duration, volume)
        current_time += duration

# Сохраняем MIDI
with open("papa_song.mid", "wb") as f:
    midi.writeFile(f)

print("Файл papa_song.mid успешно создан!")

