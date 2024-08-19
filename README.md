#import arcade
from pprint import pprint

print( "Учёт товаров")

class Product ():
    # Product('Potato', 50.0, 'Vagetables')
    def __init__(self, name, weight, category ):
        self.name  = name
        self.weight  = weight
        self.category  = category

    def __str__(self):
        return self.name + ", " + str(self.weight) + ", " + self.category + "\n"

class Shop():
    __file_name = 'products.txt'

    def get_products(self):

        file = open(self.__file_name,  'r')

        i = 0
        a = file.read()

#      while a:  # Оставим на будущее поковырять, ТЗ не оптимально ---выгружать одну базу одной строкой очень такое себе на больших базах.
#          good = a.split(', ')
#            print(good[0])
#            a = file.read()

        file.close()
        return a


    def add(self, *products):
        base = self.get_products()
        base_split = base.split('\n')

        file = open(self.__file_name,  'a')   # открываем файл на допись завозимого

        have = []

        for good in base_split: # а теперь то же самое c имеющимися на складе
            good_name = good.split(", ")
            if  good_name[0] != '':
                have.append (good_name[0] )

        for product in products:  # Обходим "неограниченное количество объектов класса Product" ищем good_name
            if  product.name in have:
                print(f'Продукт {product.name}  уже есть в магазине')
            else:
                file.write(product.__str__() )
                print(f'Продукт {product.name}  еще не было в магазине, добавляю.')

        file.close()




s1 = Shop()
p1 = Product('Potato', 50.5, 'Vegetables')
p2 = Product('Spaghetti', 3.4, 'Groceries')
p3 = Product('Potato', 5.5, 'Vegetables')
p4 = Product('Salmon', 0.12, 'fish')

print(p2) # __str__

s1.add(p1, p2, p3, p4)

#print(s1.get_products())
