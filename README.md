requirements.txt
import requests 
URL = "https://openlibrary.org/works/OL4501700W/Gale_Warning" 
r = requests.get(URL) 
print(r.content)
import requests 
from bs4 import BeautifulSoup 
import csv 

URL = "https://openlibrary.org/works/OL4501700W/Gale_Warning" 
r = requests.get(URL) 

soup = BeautifulSoup(r.content, 'html5lib') 


  books = soup.find_all('div', class_='book')
    book_info_list = []

    for book in books:
        title = book.find('h2', class_='book-title').text
        author = book.find('p', class_='book-author').text.replace('Author: ', '')
        year = book.find('p', class_='book-year').text.replace('Year: ', '')
        book_info_list.append({'Title': title, 'Author': author, 'Year': year})

    return book_info_list

def main():
    file_path = 'books.html'
    books_info = extract_books_info(file_path)

    # Print the extracted information
    for book in books_info:
        print(f"Title: {book['Title']}")
        print(f"Author: {book['Author']}")
        print(f"Year: {book['Year']}")
        print('---')

if __name__ == '__main__':
    main()

