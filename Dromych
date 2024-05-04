-import requests
import random
import bs4 
import telebot
from bs4 import BeautifulSoup as b

URL= 'https://www.anekdot.ru/last/good/'
API_KEY= '7196438433:AAGVVTZl23_ouTfik6EhX5QBHeJZRzlL_fY'
def parser(url):
  r=requests.get(url)
  soup=b(r.text, 'html.parser')
  shutka= soup.find_all('div', class_='text')
  return [c.text for c in shutka]
  
list_of_jokes=parser(URL)
random.shuffle(list_of_jokes)

bot = telebot.TeleBot(API_KEY)
@bot.message_handler(commands=['погнали'])
#Нужно установить pip install PyTelegramBotAPI

def hello(message):
    bot.send_message(message.chat.id, 'Доброго времени суток! Чтобы почитать свежие анекдоты, введите любую цифру:')
    
@bot.message_handler(content_types=['text'])
def jokes(message):
    if message.text.lower() in '123456789':
        bot.send_message(message.chat.id, list_of_jokes[0])
        del list_of_jokes[0]
    else:
        bot.send_message(message.chat.id, 'Извините! Нужно ввести именно цифру:')

bot.polling()
