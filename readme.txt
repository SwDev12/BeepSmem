Описание шагов добавления beep и smem.
1) Создаем папку sb, клонируем в него репозиторий.
git clone git://git.buildroot.net/buildroot
2)Согласно сайта последний стабильный выпуск - 31.05.2016. Просмотрим таги.
git tag
В списке есть 2016.05 .
Создаем на его основе собственную ветку и встаем на неё.
git branch my2016.05 2016.05;git checkout my2016.05
3)Копируем необходимый конфиг в корневую директорию buildroot.
cp configs/qemu_arm_versatile_defconfig .config
4) Следующая команда должна добавить в конфиг поля по дефолту
make menuconfig
Ткаже можно определить разные параметры для сборки - компилятор, библиотеки, загрузчик и прочее. Нажимаем срхранить и выйти.
5)Далее добавим наши пакеты.
В каталоге package созадем директории beep и smem.
Добавляем туда соответствующие файлы Config.in.
Оба данных файла добавляем в package/Config.in.
source "package/beep/Config.in"
source "package/smem/Config.in"
Нужно для правильного обновленного меню.
6)Добавляем .mk файлы в соответствующие директории.
7)Билдим проект.
make menuconfig
Выбор наших программ.
make
8)Результат билда.
echo $?
9)Проверка пакетов (то что они сбилдились.).
ls output/build/beep
ls output/build/smem
В директориях будет много файлов.
10)Сделаем патч в формате принятом в открытых проектах.
git format-patch master..my2016.05
Образуется файл 0001-Added-files-for-beep-and-smem-working.patch
11)На сайте github создаем репозиторий BeepSmem.github .
Создаем пустой в папке sand
mkdir sand
cp 0001-Added-files-for-beep-and-smem-working.patch ./sand
cd sand
git init
git add 0001-Added-files-for-beep-and-smem-working.patch
git commit -m "Changes in buildroot"
git remote set-url origin git@github.com:SwDev12/BeepSmem.git
git push -u origin master
12)Изменения опубликованы на сервере. Можно найти по github->search Enter SwDev12


.