from aiogram import Bot, Dispatcher, types from aiogram.utils import executor from aiogram.types import ChatMemberStatus import logging

7820524526:AAF8LQj6tnmfsNlji2jnFMfpCi8_o_J4jcc

TOKEN = "7820524526:AAF8LQj6tnmfsNlji2jnFMfpCi8_o_J4jcc"

Majburiy obuna kanali

CHANNEL = "@Ani_Freaks_uz"

bot = Bot(7820524526:AAF8LQj6tnmfsNlji2jnFMfpCi8_o_J4jcc) dp = Dispatcher(bot) logging.basicConfig(level=logging.INFO)

async def check_subscription(user_id): chat_member = await bot.get_chat_member(CHANNEL, user_id) return chat_member.status in [ChatMemberStatus.MEMBER, ChatMemberStatus.OWNER, ChatMemberStatus.ADMINISTRATOR]

@dp.message_handler(commands=['start']) async def start_cmd(message: types.Message): user_id = message.from_user.id is_subscribed = await check_subscription(user_id)

if not is_subscribed:
    await message.answer(f"Salom! Botdan foydalanish uchun avval {@Ani_Freaks_uz} kanaliga obuna bo‘lishingiz kerak!", 
                         reply_markup=types.InlineKeyboardMarkup().add(
                             types.InlineKeyboardButton("📢 Kanalga obuna bo‘lish", url=f"https://t.me/{@Ani_Freaks_uz[1:]}")
                         ))
else:
    await message.answer("✅ Obuna tasdiqlandi! Endi anime yuklash mumkin.")

@dp.message_handler(content_types=['document', 'video', 'photo']) async def handle_files(message: types.Message): user_id = message.from_user.id is_subscribed = await check_subscription(user_id)

if not is_subscribed:
    await message.answer(f"Botdan foydalanish uchun avval {@Ani_Freaks_uz} kanaliga obuna bo‘ling!")
    return

await message.forward(@Ani_Freaks_uz)  # Faylni kanalga yuborish
await message.answer("✅ Anime muvaffaqiyatli yuklandi!")

if name == 'main': executor.start_polling(dp)


