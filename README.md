# Text_File_Metadata
📁 Extract metadata from .txt files and record the metadata in .txt files.
#

![Receipt 1](https://github.com/sourceduty/Text_File_Metadata/assets/123030236/6bb4d9db-0c8d-40eb-84c1-f3d1ff24f51e)

![WordFrequency_First txt](https://github.com/sourceduty/Text_File_Metadata/assets/123030236/e6c4e78e-2875-414d-8de5-9e41c2410503)

```
import os
import sys
from collections import Counter
import matplotlib.pyplot as plt
import webbrowser

path = 'Folder1'
contents_list = []

for filename in filter(lambda p: p.endswith(".txt"), os.listdir(path)):
    filepath = os.path.join(path, filename)
    with open(filepath, mode='r') as meta_file:
        contents_list += [meta_file.read()]

    with open('Metadata.txt', 'w') as meta_file:
        sys.stdout = meta_file
        print(contents_list)

    with open(filepath, mode='r') as f:
        contents = f.read()
        words = contents.split()
        total_word_count = len(words)

        word_counter = Counter(words)
        most_common_words = word_counter.most_common()

        analysis_filename = f"Analysis_{filename}"
        with open(analysis_filename, 'w') as analysis_file:
            sys.stdout = analysis_file
            print("Total number of words:", total_word_count)
            print("\nRecurring words:")
            for word, count in most_common_words:
                print(f"{word}: {count}")

        top_words = 20
        top_words_data = most_common_words[:top_words]
        words, counts = zip(*top_words_data)

        plt.figure(figsize=(10, 6))
        plt.bar(words, counts)
        plt.title(f"Top {top_words} Most Common Words in {filename}")
        plt.xlabel("Words")
        plt.ylabel("Frequency")
        plt.xticks(rotation=45)
        plt.tight_layout()

        figure_filename = f"WordFrequency_{filename}.png"
        plt.savefig(figure_filename)
        plt.close()
        webbrowser.open(figure_filename)
```
#
ℹ️ This software is free and open-source; anyone can redistribute it and/or modify it.
