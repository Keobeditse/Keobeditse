beautifulsoup4
lxml
__pycache__/
*.pyc
venv/


def parse_user_info(file_path):
    users = []
    with open(file_path, 'r', encoding='utf-8') as file:
        lines = file.readlines()

    current_user = {}
    for line in lines:
        line = line.strip()
        if line == '':
            if current_user:
                users.append(current_user)
                current_user = {}
        else:
            key, value = line.split(': ', 1)
            current_user[key] = value

    if current_user:
        users.append(current_user)

    return users

def main():
    file_path = 'users.txt'
    users = parse_user_info(file_path)

    for user in users:
        print(f"Name: {user.get('Name', 'N/A')}")
        print(f"Age: {user.get('Age', 'N/A')}")
        print(f"Occupation: {user.get('Occupation', 'N/A')}")
        print('---')

if __name__ == '__main__':
    main()

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python extract_info.py

