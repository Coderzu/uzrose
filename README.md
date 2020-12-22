# Marie-2.0-Uzbek
Sqlalchemy ma'lumotlar bazasi bilan python3 da ishlaydigan modulli telegram Python bot.

Dastlab bir nechta administrator xususiyatlariga ega bo'lgan oddiy guruh boshqaruvi boti rivojlanib, nihoyatda modulli va
ishlatish uchun oddiy.

Telegramda [Rose](https://t.me/uzRoseBot) nomi bilan topish mumkin.

Mari va men [qo'llab-quvvatlash guruhini](https://t.me/dizaynerlar_guruhi) boshqaramiz, bu yerda siz o'zingizning qurilmangizni o'rnatishda yordam so'rashingiz mumkin
bot, yangi xususiyatlarni kashf eting / so'rang, xatolar haqida xabar bering va har doim yangi bo'lib turing

Agar siz faqat yangi xususiyatlar haqida xabardor bo'lishni istasangiz [yangiliklar kanaliga](https://t.me/pixellab_tutorials) qo'shiling
e'lonlar.

Shu bilan bir qatorda, [meni telegramda toping](https://t.me/kassir)! (Qo'llab-quvvatlash bo'yicha barcha savollarni qo'llab-quvvatlash chatida saqlang, bu erda sizga ko'proq odamlar yordam berishi mumkin.)

##Bundan tashqari, to'g'ridan-to'g'ri Heroku-ga o'tish uchun quyida joylashgan "Heroku-ga o'tish" tugmachasini bosishingiz mumkin!

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/FunBirdUz/uzrose)

## Botni ishga tushirish.

Ma'lumotlar bazasini o'rnatganingizdan so'ng va sizning konfiguratsiyangiz (pastga qarang) tugallangandan so'ng, shunchaki bajaring:

`python3 -m tg_bot`


##Botni sozlash (Buni ishlatishdan oldin o'qing!):
Iltimos, python3.6 dan foydalanganingizga ishonch hosil qiling, chunki men hamma narsa eski python versiyalarida kutilganidek ishlashiga kafolat berolmayman!
Buning sababi shundaki, markdownni ajratish 3.6-da sukut bo'yicha buyurtma qilingan dikt orqali takrorlash orqali amalga oshiriladi.

### Konfiguratsiya

Botni sozlashning ikkita usuli mavjud: config.py fayli yoki ENV o'zgaruvchilari.

"Config.py" faylidan foydalanish afzalroq, chunki bu sizning barcha sozlamalaringizni birlashtirilganligini ko'rishni osonlashtiradi.
Ushbu fayl "tg_bot" papkasida, "__main __.py`" fayli bilan birga joylashtirilishi kerak. 
Bu erda sizning bot belgingiz, shuningdek ma'lumotlar bazasi URI (agar siz ma'lumotlar bazasidan foydalanayotgan bo'lsangiz) va ko'pchiligidan yuklanadi.
boshqa sozlamalaringiz.

Sample_config faylini import qilish va Config sinfini kengaytirish tavsiya etiladi, chunki bu sizning konfiguratsiyangiz barchasini o'z ichiga oladi
default_ sample_config-da o'rnatilgan bo'lib, yangilanishni osonlashtiradi.

Masalan, "config.py" fayli quyidagicha bo'lishi mumkin:
```
from tg_bot.sample_config import Config


class Development(Config):
    OWNER_ID = 352040593  # my telegram ID
    OWNER_USERNAME = "Anandus"  # my telegram username
    API_KEY = "your bot api key"  # my api key, as provided by the botfather
    SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost:5432/database'  # sample db credentials
    MESSAGE_DUMP = '-1234567890' # some group chat that your bot is a member of
    USE_MESSAGE_DUMP = True
    SUDO_USERS = [738438054, 352040593]  # List of id's for users which have sudo access to the bot.
    LOAD = []
    NO_LOAD = ['translation']
```

Agar config.py fayliga ega bo'lmasangiz (EG on heroku), atrof muhit o'zgaruvchilaridan ham foydalanish mumkin.
Quyidagi env o'zgaruvchilari qo'llab-quvvatlanadi:
 - `ENV`: Buni ANYTHING-ga o'rnatish env o'zgaruvchilarini yoqadi

 - `TOKEN`: Sizning stringiz sifatida bot tokeni
 - `OWNER_ID`: Sizning ID raqamingiz
 - `OWNER_USERNAME`: Usernameingiz

 - `DATABASE_URL`: Sizning ma'lumotlar bazangiz URL manzili
 - `MESSAGE_DUMP`: ixtiyoriy: odamlar eskisini o'chirishni to'xtatish uchun sizning javobli saqlangan xabarlaringiz saqlanadigan suhbat 
 - `LOAD`: Space separated list of modules you would like to load
 - `NO_LOAD`: Space separated list of modules you would like NOT to load
 - `WEBHOOK`: Setting this to ANYTHING will enable webhooks when in env mode
 messages
 - `URL`: The URL your webhook should connect to (only needed for webhook mode)

 - `SUDO_USERS`: A space separated list of user_ids which should be considered sudo users
 - `SUPPORT_USERS`: A space separated list of user_ids which should be considered support users (can gban/ungban,
 nothing else)
 - `WHITELIST_USERS`: A space separated list of user_ids which should be considered whitelisted - they can't be banned.
 - `DONATION_LINK`: Optional: link where you would like to receive donations.
 - `CERT_PATH`: Path to your webhook certificate
 - `PORT`: Port to use for your webhooks
 - `DEL_CMDS`: Whether to delete commands from users which don't have rights to use that command
 - `STRICT_GBAN`: Enforce gbans across new groups as well as old groups. When a gbanned user talks, he will be banned.
 - `WORKERS`: Number of threads to use. 8 is the recommended (and default) amount, but your experience may vary.
 __Note__ that going crazy with more threads wont necessarily speed up your bot, given the large amount of sql data 
 accesses, and the way python asynchronous calls work.
 - `BAN_STICKER`: Which sticker to use when banning people.
 - `ALLOW_EXCL`: Whether to allow using exclamation marks ! for commands as well as /.

### Python dependencies

Install the necessary python dependencies by moving to the project directory and running:

`pip3 install -r requirements.txt`.

This will install all necessary python packages.

### Database

If you wish to use a database-dependent module (eg: locks, notes, userinfo, users, filters, welcomes),
you'll need to have a database installed on your system. I use postgres, so I recommend using it for optimal compatibility.

In the case of postgres, this is how you would set up a the database on a debian/ubuntu system. Other distributions may vary.

- install postgresql:

`sudo apt-get update && sudo apt-get install postgresql`

- change to the postgres user:

`sudo su - postgres`

- create a new database user (change YOUR_USER appropriately):

`createuser -P -s -e YOUR_USER`

This will be followed by you needing to input your password.

- create a new database table:

`createdb -O YOUR_USER YOUR_DB_NAME`

Change YOUR_USER and YOUR_DB_NAME appropriately.

- finally:

`psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

This will allow you to connect to your database via your terminal.
By default, YOUR_HOST should be 0.0.0.0:5432.

You should now be able to build your database URI. This will be:

`sqldbtype://username:pw@hostname:port/db_name`

Replace sqldbtype with whichever db youre using (eg postgres, mysql, sqllite, etc)
repeat for your username, password, hostname (localhost?), port (5432?), and db name.

## Modules
### Setting load order.

The module load order can be changed via the `LOAD` and `NO_LOAD` configuration settings.
These should both represent lists.

If `LOAD` is an empty list, all modules in `modules/` will be selected for loading by default.

If `NO_LOAD` is not present, or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file be in the modules folder.

To add commands, make sure to import the dispatcher via

`from tg_bot import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user
friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so 
it is necessary to migrate it in the db.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed 
through the `/stats` command, which is only available to the bot owner.
