# Этот бот был сделан по приколу, чтобы разобраться как в общем такое делается
#////////////////////////////////////////////
import telebot

from telebot import types
bot = telebot.TeleBot('6923951992:AAHmMt2_3aS81LvAPL0XkkLau1-f2YdQ0CY')

import random

@bot.message_handler(commands=['Start'])
def start(message):
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True, row_width=2)
    website = types.KeyboardButton('/Website')
    start = types.KeyboardButton('/Start')
    photo = types.KeyboardButton('/LogoPhoto')
    fun = types.KeyboardButton('/Fun')
    markup.add(start,website, photo,fun)
    mess = f'Здаров, <b><u>{message.from_user.first_name}</u></b>'
    bot.send_message(message.chat.id, mess, parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['LogoPhoto'])
def get_user_photo(message):
    photo = open('logo.jpg', 'rb')
    bot.send_photo(message.chat.id, photo)
    @bot.message_handler(commands=['Website'])
def website(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton("Четкий сайт", "https://youtu.be/dQw4w9WgXcQ?si=6LHt0lUwxp5ap0rq"))
    bot.send_message(message.chat.id, 'Ссылка в описании', reply_markup=markup)

@bot.message_handler(commands=['Fun'])
def word_smart(message):
    word_list = ["Видит наркоман, как араб выбивает ковер, подходит к нему и говорит:\n"
                 "-Че бл*ть, не заводится?",
                 "-Сегодня утром понял, что мой холодильник-девочка\n"
                 " -Это как?\n"
                 " -Яиц нет!",
                 "Уха-ха-ха-ха:-сказала лягушка",
                 "-Извините, а у вас огоньку не найдется?\n"
                 "-Да иди ты н**уй, - ответил медведь из машины",
                 "-Пончик, пончик: кричали дети колобку, не подозревая что он серьёзно ранен",
                 "Утром мама будит сына:\n"
                 "-Сынок, вставай!\n"
                 "-Зачем, мам у нас же сегодня выходной!\n"
                 "-Какой к черту выходной?! Мы же негры!",
                 "-Знаете что общего у пчелы и инвалида-колясочника?\n"
                 "-Нет, не знаю!\n"
                 "-Жалко",
                 "Глупый человек жалуется на дырку в кармане, а мудрый использует ее чтобы почесать себе яйца"]
    random_word = random.choice(word_list)
    bot.send_message(message.chat.id, f"Шутка от бота:\n {random_word}")

bot.polling(none_stop=True)
