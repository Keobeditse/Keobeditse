from bs4 import BeautifulSoup


with open('requirements.txt', 'r') as file:
    html_content = file.read()


soup = BeautifulSoup(html_content, 'lxml')

products = soup.find_all('div', class_='product')

for product in products:
    name = product.find('h2', class_='product-name').text
    price = product.find('p', class_='product-price').text
    rating = product.find('p', class_='product-rating').text
    
    print(f"Product Name: {name}")
    print(f"Price: {price}")
    print(f"Rating: {rating}")
    print('---')

