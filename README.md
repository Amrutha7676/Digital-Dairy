# Digital-Dairy
import datetime

class Diary:
    def __init__(self, filename="diary.txt"):
        self.filename = filename

    def write_entry(self):
        entry = input("Write your diary entry:\n")
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        with open(self.filename, "a") as file:
            file.write(f"\n[{timestamp}]\n{entry}\n")
        print("✅ Entry saved successfully!")

    def view_entries(self):
        try:
            with open(self.filename, "r") as file:
                content = file.read()
                if content:
                    print("\n📝 Your Diary Entries:\n")
                    print(content)
                else:
                    print("🚫 No entries found.")
        except FileNotFoundError:
            print("🚫 Diary file not found.")

    def search_entries(self, keyword):
        try:
            with open(self.filename, "r") as file:
                lines = file.readlines()
                print(f"\n🔍 Search Results for '{keyword}':\n")
                found = False
                for i in range(len(lines)):
                    if keyword.lower() in lines[i].lower():
                        found = True
                        print(''.join(lines[i:i+2]))
                if not found:
                    print("🚫 No matching entries found.")
        except FileNotFoundError:
            print("🚫 Diary file not found.")

def main():
    diary = Diary()
    while True:
        print("\n--- Digital Diary ---")
        print("1. Write a new entry")
        print("2. View all entries")
        print("3. Search diary")
        print("4. Exit")

        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            diary.write_entry()
        elif choice == "2":
            diary.view_entries()
        elif choice == "3":
            keyword = input("Enter a keyword or date (YYYY-MM-DD): ")
            diary.search_entries(keyword)
        elif choice == "4":
            print("👋 Goodbye!")
            break
        else:
            print("❗ Invalid choice. Try again.")

if __name__ == "__main__":
    main()
