"""
Web Scraper for News Headlines
Using only built-in libraries (works in Programiz)
"""

import urllib.request
from html.parser import HTMLParser


URL = "https://www.bbc.com/news"
OUTPUT_FILE = "headlines.txt"


class HeadlineParser(HTMLParser):
    def __init__(self):
        super().__init__()
        self.inside_h2 = False
        self.headlines = []

    def handle_starttag(self, tag, attrs):
        if tag == "h2":
            self.inside_h2 = True

    def handle_endtag(self, tag):
        if tag == "h2":
            self.inside_h2 = False

    def handle_data(self, data):
        if self.inside_h2:
            text = data.strip()
            if text and text not in self.headlines:
                self.headlines.append(text)


def main():
    try:
        response = urllib.request.urlopen(URL)
        html = response.read().decode("utf-8")

        parser = HeadlineParser()
        parser.feed(html)

        # Save first 10 headlines
        with open(OUTPUT_FILE, "w", encoding="utf-8") as file:
            for i, headline in enumerate(parser.headlines[:10], 1):
                file.write(f"{i}. {headline}\n")

        print("Headlines saved successfully!")

    except Exception as e:
        print("Error:", e)


if __name__ == "__main__":
    main()
