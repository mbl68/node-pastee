DATA = 0


print(" 👑SilkRoad👑 (سلك رود)")
GLabel = "OneState"
GProcess = "com.Chillgaming.oneState"

if gg.getTargetInfo().processName ~= GProcess then
  gg.alert("هذا سكربت مخصص لـ:\n" .. GLabel .. "\n" .. GProcess .. [[


لقد اخترت:
]] .. gg.getTargetInfo().label .. "\n" .. gg.getTargetInfo().processName)
  os.exit()
  return
end 

function TesterLua()
  local L0_0, L1_1
end 

function search(class, offset, tryHard, bit32, valueType)
Get_user_input = {}
Get_user_input[1] = class
Get_user_input[2] = offset
Get_user_input[3] = tryHard
Get_user_input[4] = bit32
Get_user_type = valueType
start()
end

function loopCheck()
if userMode == 1 then
UI()
elseif error == 3 then
os.exit()
end
end

function found_(message)
if error == 1 then
found2(message)
elseif error == 2 then
found3(message)
elseif error == 3 then
found4(message)
else
found(message)
end
end

function found(message)
if count == 0 then
gg.clearResults()
gg.clearList()
first_error = message
error = 1
second_start()
end
end

function found2(message)
if count == 0 then
gg.clearResults()
gg.clearList()
second_error = message
error = 2
third_start()
end
end

function found3(message)
if count == 0 then
gg.clearResults()
gg.clearList()
third_error = message
error = 3
fourth_start()
end
end

function found4(message)
if count == 0 then
gg.clearResults()
gg.clearList()
gg.setVisible(true)
gg.alert("❌ لم يتم العثور على القيمة ❌")
loopCheck()
end
end

function user_input_taker()
::stort::
gg.clearResults()
if userMode == 1 then
if Get_user_input == nil then
default1 = "PlayerController"
default2 = "0x148"
default3 = false
default4 = false
else
default1 = Get_user_input[1]
default2 = Get_user_input[2]
default3 = Get_user_input[3]
default4 = Get_user_input[4]
end
Get_user_input = gg.prompt(
{"Class Name: ", "Offset: ","Try Harder -- (decreases accuracy)","Try For 32 bit"},
{default1,default2,default3,default4},
{"text","text","checkbox","checkbox"})
if Get_user_input ~= nil then
if (Get_user_input[1] == "") or (Get_user_input[2] == "") then
gg.alert("ℹ️ لا تترك الإدخال فارغًا ℹ️")
goto stort
end
else
gg.alert("ℹ️ خطأ: حاول مرة أخرى ℹ️")
goto stort
end
Get_user_type = gg.choice({"1. Byte / Boolean","2. Dword / 32 bit Int","3. Qword / 64 bit Int","4. Float","5. Double"})
if Get_user_type == 1 then
Get_user_type = gg.TYPE_BYTE
elseif Get_user_type == 2 then
Get_user_type = gg.TYPE_DWORD
elseif Get_user_type == 3 then
Get_user_type = gg.TYPE_QWORD
elseif Get_user_type == 4 then
Get_user_type = gg.TYPE_FLOAT
elseif Get_user_type == 5 then
Get_user_type = gg.TYPE_DOUBLE
end
if Get_user_type ~= gg.TYPE_BYTE then
if (Get_user_input[2] % 4) ~= 0 then
gg.alert("ℹ️يجب أن تكون الإزاحة السداسية مضاعفًا لـ 4ℹ️")
goto stort
end
end
end
error = 0 
end

function O_initial_search()
gg.setVisible(false)
gg.toast("🟢 محاوله الأولى")
user_input = ":"..Get_user_input[1] 
if Get_user_input[3] then
offst = 25
else
offst = 0
end
end

function O_dinitial_search()
if error > 1 then
gg.setRanges(gg.REGION_C_ALLOC)
else
gg.setRanges(gg.REGION_OTHER)
end
gg.searchNumber(user_input, gg.TYPE_BYTE)
count = gg.getResultsCount()
if count == 0 then
found_("O_dinitial_search")
return 0
end
Refiner = gg.getResults(1)
gg.refineNumber(Refiner[1].value, gg.TYPE_BYTE)
count = gg.getResultsCount()
if count == 0 then
found_("O_dinitial_search")
return 0
end
val = gg.getResults(count)
gg.addListItems(val)
end

function CA_pointer_search()
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
gg.loadResults(gg.getListItems())
gg.searchPointer(offst)
count = gg.getResultsCount()
if count == 0 then
found_("CA_pointer_search")
return 0
end
vel = gg.getResults(count)
gg.clearList()
gg.addListItems(vel)
end

function CA_apply_offset()
if Get_user_input[4] then
tanker = 0xfffffffffffffff8
else
tanker = 0xfffffffffffffff0
end
local copy = false
local l = gg.getListItems()
if not copy then gg.removeListItems(l) end
for i, v in ipairs(l) do
	v.address = v.address + tanker
	if copy then v.name = v.name..' #2' end
end
gg.addListItems(l)
end

function CA2_apply_offset()
if Get_user_input[4] then
tanker = 0xfffffffffffffff8
else
tanker = 0xfffffffffffffff0
end
local copy = false
local l = gg.getListItems()
if not copy then gg.removeListItems(l) end
for i, v in ipairs(l) do
	v.address = v.address + tanker
	if copy then v.name = v.name..' #2' end
end
gg.addListItems(l)
end

function Q_apply_fix()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.loadResults(gg.getListItems())
gg.clearList()
count = gg.getResultsCount()
if count == 0 then
found_("Q_apply_fix")
return 0
end
yy = gg.getResults(1000)
gg.clearResults()
i = 1
c = 1
s = {}
while (i-1) < count do
yy[i].address = yy[i].address + 0xb400000000000000
gg.searchNumber(yy[i].address, gg.TYPE_QWORD)
cnt = gg.getResultsCount()
if 0 < cnt then
bytr = gg.getResults(cnt)
n = 1
while (n-1) < cnt do
s[c] = {}
s[c].address = bytr[n].address
s[c].flags = 32
n = n + 1
c = c + 1
end
end
gg.clearResults()
i = i + 1
end
gg.addListItems(s)
end

function A_base_value()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.loadResults(gg.getListItems())
gg.clearList()
gg.searchPointer(offst)
count = gg.getResultsCount()
if count == 0 then
found_("A_base_value")
return 0
end
tel = gg.getResults(count)
gg.addListItems(tel)
end

function A_base_accuracy()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_ALLOC)
gg.loadResults(gg.getListItems())
gg.clearList()
gg.searchPointer(offst)
count = gg.getResultsCount()
if count == 0 then
found_("A_base_accuracy")
return 0
end
kol = gg.getResults(count)
i = 1
h = {}
while (i-1) < count do
h[i] = {}
h[i].address = kol[i].value
h[i].flags = 32
i = i + 1
end
gg.addListItems(h)
end

function A_user_given_offset()
local old_save_list = gg.getListItems()
for i, v in ipairs(old_save_list) do
v.address = v.address + Get_user_input[2]
v.flags = Get_user_type
end
gg.clearResults()
gg.clearList()
gg.loadResults(old_save_list)
count = gg.getResultsCount()
if count == 0 then
found_("Q_apply_fix++")
return 0
end
end

function start()
user_input_taker()
O_initial_search()
O_dinitial_search()
if error > 0 then
return 0
end
CA_pointer_search()
if error > 0 then
return 0
end
CA_apply_offset()
if error > 0 then
return 0
end
A_base_value()
if error > 0 then
return 0
end
if offst == 0 then
A_base_accuracy()
end
if error > 0 then
return 0
end
A_user_given_offset()
if error > 0 then
return 0
end
loopCheck()
if error > 0 then
return 0
end
end

function second_start()
gg.toast("🟡 محاوله ثانيه")
O_dinitial_search()
if error > 1 then
return 0
end
CA_pointer_search()
if error > 1 then
return 0
end
CA_apply_offset()
if error > 1 then
return 0
end
Q_apply_fix()
if error > 1 then
return 0
end
if offst == 0 then
A_base_accuracy()
end
if error > 1 then
return 0
end
A_user_given_offset()
if error > 1 then
return 0
end
loopCheck()
if error > 1 then
return 0
end
end

function third_start()
gg.toast("🔴 محاوله ثالثه")
O_dinitial_search()
if error > 2 then
return 0
end
CA_pointer_search()
if error > 2 then
return 0
end
if offst == 0 then
CA2_apply_offset()
end
if error > 2 then
return 0
end
A_base_value()
if error > 2 then
return 0
end
if offst == 0 then
A_base_accuracy()
end
if error > 2 then
return 0
end
A_user_given_offset()
if error > 2 then
return 0
end
loopCheck()
if error > 2 then
return 0
end
end

function fourth_start()
gg.toast("☢️محاوله رابعه")
O_dinitial_search()
CA_pointer_search()
CA2_apply_offset()
Q_apply_fix()
if offst == 0 then
A_base_accuracy()
end
A_user_given_offset()
loopCheck()
end

function UI()
gg.showUiButton()
while true do
if gg.isClickedUiButton() then
start()
end
end
end



-- المتغيرات العامة
local HR = -1
local currentCenterAddr = 0
local freezeEdit = false
local storageFile = "/sdcard/teleport_saved.txt"
local customList = {}

-- اختيار اللغة
local LANGUAGES = {"🇮🇶 العربية", "🇬🇧 English", "🇹🇷 Türkçe"}
local langCode = {"ar", "en", "tr"}
local L = gg.choice(LANGUAGES, nil, "❖ اختر اللغة / Select Language / Dil Seçin")
if not L then os.exit() end
local lang = langCode[L]

-- جدول النصوص
local messages = {
  prompt = {
    ar = "🔐  هذا الباسورد 👉🏻SilkRoad",
    en = "🔐SilkRoad",
    tr = "🔐SilkRoad"
  },
  incorrect_code = {
    ar = "❌  سلك رود",
    en = "❌ SilkRoad.",
    tr = "❌ https://t.me/T1Wbm"
  },
  expired_code = {
    ar = "⛔ انتهت صلاحية هذا الرمز. تواصل مع https://t.me/T1Wbm على تيليجرام لتجديده. ",
    en = "⛔ This code has expired. Contact https://t.me/T1Wbm Telegram to renew. ",
    tr = "⛔ Bu kodun süresi doldu. Yenilemek için  Telegram ile iletişime geçin. "
  },
  tamper_detected = {
    ar = "❌  انا صاحب هذا السكريبت الاصلي\nSilkRoad",
    en = "❌ Device date has been tampered.\nPlease set the correct date.",
    tr = "❌ Cihaz tarihi ile oynanmış.\nLütfen doğru tarihi ayarlayın."
  },
  success = {
    ar = "✅ تم التفعيل بنجاح! مرحبًا بك.",
    en = "✅ Activation successful! Welcome.",
    tr = "✅ Aktivasyon başarılı! Hoş geldiniz."
  }
}

-- إعدادات الكود والتاريخ
local correctCode = "SilkRoad"
local expiryDate = { day = 30, month = 10, year = 2070 }
local expiryHour = 18  -- الساعة 6 مساءً
local expiryMinute = 0
local timePath = "/storage/emulated/0/Android/.activation_time.txt"
gg.copyText("SilkRoad")
-- كتابة أول وقت تشغيل
function writeFirstTime()
  local f = io.open(timePath, "w")
  if f then
    f:write(os.time())
    f:close()
  end
end

-- قراءة الوقت المسجل
function readFirstTime()
  local f = io.open(timePath, "r")
  if f then
    local savedTime = tonumber(f:read("*a"))
    f:close()
    return savedTime
  end
  return nil
end

-- هل تم التلاعب بالتاريخ؟
function isTampered(current, saved)
  return current < saved
end

-- هل انتهت صلاحية الكود؟
function isExpired(current, expiry)
  if current.year > expiry.year then
    return true
  elseif current.year == expiry.year and current.month > expiry.month then
    return true
  elseif current.year == expiry.year and current.month == expiry.month and current.day > expiry.day then
    return true
  elseif current.year == expiry.year and current.month == expiry.month and current.day == expiry.day then
    if current.hour > expiryHour then
      return true
    elseif current.hour == expiryHour and current.min >= expiryMinute then
      return true
    end
  end
  return false
end

-- دالة التحقق من التفعيل
function checkActivation()
  -- إدخال الكود
  local input = gg.prompt({messages.prompt[lang]}, nil, {"text"})
  if not input then os.exit() end

  -- التحقق من الكود
  if input[1] ~= correctCode then
    gg.alert(messages.incorrect_code[lang])
    os.exit()
  end

  -- التحقق من التلاعب بالتاريخ
  local currentUnix = os.time()
  local firstTime = readFirstTime()
  if not firstTime then
    writeFirstTime()
  elseif isTampered(currentUnix, firstTime) then
    gg.alert(messages.tamper_detected[lang])
    os.exit()
  end

  -- التحقق من انتهاء الصلاحية
  local currentDate = os.date("*t")
  if isExpired(currentDate, expiryDate) then
    gg.alert(messages.expired_code[lang] ..
      expiryDate.day .. "/" .. expiryDate.month .. "/" .. expiryDate.year ..
      " - الساعة " .. string.format("%02d:%02d", expiryHour, expiryMinute))
    os.exit()
  end

local messages = {
  success = {
    ar = "✅ تم التفعيل بنجاح!",
    en = "✅ Activation successful!",
    tr = "✅ Aktivasyon başarılı!"
  },
  copy_alert = {
    ar = "SilkRoad\nSilkRoad",
    en = "📢 https://t.me/T1Wbm اشتركوا بقناتنا تيليجرام\n",
    tr = "📢  telegram 👑🇮🇶🇩🇿👑🇮🇶SilkRoad🇩🇿👑"
  },
  copied = {
    ar = "تم نسخ روابط القناة والتيك توك، يمكنك لصقها في أي مكان.",
    en = "Channel & TikTok links copied, you can paste anywhere.",
    tr = "Kanal ve TikTok linkleri kopyalandı, istediğiniz yere yapıştırabilirsiniz."
  }
}

-- ✅ تم التفعيل بنجاح
gg.toast(messages.success[lang])

-- نص روابط القناة والتيك توك حسب اللغة
local infoText = messages.copy_alert[lang]

-- عرض التنبيه مع النص حسب اللغة
gg.alert(infoText)

-- نسخ روابط القناة التيليجرام فقط (يمكنك تعديلها لتشمل أكثر إذا تريد)
local toCopy = "https://t.me/T1Wbm"
gg.copyText(toCopy)

-- رسالة تفيد بنسخ الرابط حسب اللغة
gg.toast(messages.copied[lang])


end

-- بدء التحقق
checkActivation()

gg.setVisible(false)
gg.setVisible(false)


local Load_Info_User = [[🇮🇶🇩🇿  Silk Road سلك رود 👑🇮🇶Silk Road🇩🇿👑]]  

gg.setVisible(true)
gg.setRanges(gg.REGION_ANONYMOUS)
off = "❌"
on = "  ✅️"
Offe = "❌️"
One = "  ✅️"
um = off
dois = off
tres = off
quatro = off
cinco = off
seis = off
sete = off
oito = off
nove = off
onze = off
dez = off
ori = off
oru = off
bob = off
epa = off
gg.toast('اهلا بك بسكربس الكرود المجاني انا صاحب هذا السكريبت سيليكرودSilkRoad👑')
function Home()
gg.copyText("👑SilkRoad👑")
  
  local mainMenu = gg.choice({
"❌️SilkRoadسرعة ",
ori .. "👑SilkRoad👑سلاح لا يحتاج إلى إعادة تحميل ",
oru .. "👑SilkRoad👑رؤية الكاميرا ",
"❌️👑SilkRoad👑النقل الجرافيتي ",
"❌️👑SilkRoad👑مواقع Tp ",
dois .. "👑SilkRoad👑دمية عملاقة ",
epa .. "دمية مصغرة",
tres .. "قدرة تحمل لا نهائية ",
nove .. "وظائف المزرعة ",
onze .. "بنك المزرعة ",
dez .. "سرقة المواد ",
cinco .. "سيارة مدرعة ",
seis .. "الهروب من السجن ",
sete .. "سيارات السرعة ",
oito .. "سيارة وول هاك ",
"❌️قائمة السيارة الطائرة ",
    "خروج💙"
  }, nil, "" .. Load_Info_User .. "")
  if mainMenu == nil then
    return
  end
  if mainMenu == 1 then
    Speed()
  end
  if mainMenu == 2 then
    NoReload()
  end
  if mainMenu == 3 then
    Ipad()
  end
  if mainMenu == 4 then
    MenuPontos()
  end
  if mainMenu == 5 then
    TpLocal()
  end
  if mainMenu == 6 then
    BonecoGigante()
  end
  if mainMenu == 7 then
    BonecoMiniatura()
  end
  if mainMenu == 8 then
    Stamina()
  end
  if mainMenu == 9 then
    FarmAll()
  end
  if mainMenu == 10 then
    FarmAllSpeed()
  end
  if mainMenu == 11 then
    Roubo()
  end
  if mainMenu == 12 then
    Collision()
  end
  if mainMenu == 13 then
    prisao()
  end
  if mainMenu == 14 then
    Velocidade()
  end
  if mainMenu == 15 then
    WallHack()
  end
  if mainMenu == 16 then
    MenuControle()
  end
  if mainMenu == 17 then
    EXITEX()
  end
end

function AimBot()
  salvar_localCamera()
  salvar_Camera()
  salvar_inimigos()
  loop_aimbot_fixo_realHead()
end

function Ipad()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 00 00 B4 43 00 00 B4 43 00 00 B4 43 00 00 B4 43", 1)
  mnovs = gg.getResults(1)
  R = gg.prompt({
    "🔎 حدد مسافة الكاميرا 🔎\n➖➖➖➖➖➖➖➖➖➖ [68 ; 170]"
  }, {
    [1] = defaultValue
  }, {
    [1] = "number"
  })
  if R == nil then
    gg.toast("تم الإلغاء")
    return
  end
  do
    do
      for _FORV_3_, _FORV_4_ in ipairs(mnovs) do
        _FORV_4_.address = _FORV_4_.address + 52
        _FORV_4_.value = R[1]
        _FORV_4_.flags = 16
      end
    end
  end
  gg.setValues(mnovs)
  Enabled_Function()
end

function TpCarro()
  emanuel = gg.choice({
"🇮🇶متجر أسلحة ",
"🇮🇶تصرف ",
"🇮🇶حاجِز ",
"🇮🇶مركز الشرطة ",
"🇮🇶صيدلية ",
"🇮🇶إكزسيتو  ",
"🇮🇶سوق المركبات ",
"🇮🇶متجر ملابس ",
"🇮🇶مستشفى ",
"🇮🇶رصيف ",
"🇮🇶رصيف سيما ",
"🇮🇶وظيفة سائق شاحنة ",
"🇮🇶مدير عام ",
"🇮🇶متجر الأسلحة 2 ",
"🇮🇶امتحان "
  }, nil, "       ╔══════◄••❀••►══════╗\n       ╠━   『مجاني』 👑  🇩🇿Silk Road  🇮🇶👑 \n       ╚══════◄••❀••►══════╝")
  if emanuel == nil then
    return
  end
  if emanuel == 1 then
    CarLojaDeArmas()
  end
  if emanuel == 2 then
    CarDescarteDeVeiculos()
  end
  if emanuel == 3 then
    CarButeco()
  end
  if emanuel == 4 then
    CarDelegacia()
  end
  if emanuel == 5 then
    CarFarmacia()
  end
  if emanuel == 6 then
    CarExecito()
  end
  if emanuel == 7 then
    CarMercadoVeiculos()
  end
  if emanuel == 8 then
    CarLojaRoupas()
  end
  if emanuel == 9 then
    CarHospital()
  end
  if emanuel == 10 then
    CarPier()
  end
  if emanuel == 11 then
    CarPierCima()
  end
  if emanuel == 12 then
    CarCaminhoneiro()
  end
  if emanuel == 13 then
    CarTpAdm()
  end
  if emanuel == 14 then
    CarLojaDeArmas2()
  end
  if emanuel == 15 then
    Carteste()
  end
end

function CarButeco()
  emanuel = gg.choice({
"🇮🇶حاجِز ",
"🇮🇶حاجِز2 "
  }, nil, "       ╔══════◄••❀••►══════╗\n       ╠━   『مجاني』 👑  Silk Road  👑 \n       ╚══════◄••❀••►══════╝")
  if emanuel == nil then
    return
  end
  if emanuel == 1 then
    Bar()
  end
  if emanuel == 2 then
    Bar2()
  end
end

function CarTpAdm()
  emanuel = gg.choice({
"🇮🇶إدارة الممتلكات ",
"🇮🇶بلدية ",
"🇮🇶ايرو1 ",
"🇮🇶ايرو2 ",
"🇮🇶ايرو3 ",
"🇮🇶ايرو4 ",
"🇮🇶ايرو5 ",
"🇮🇶ايرو6 ",
"🇮🇶إكزسيتو 1",
"🇮🇶إكزسيتو 2"
  }, nil, "       ╔══════◄••❀••►══════╗\n       ╠━   『مجاني』 👑  Silk Road  👑 \n       ╚══════◄••❀••►══════╝")
  if emanuel == nil then
    return
  end
  if emanuel == 1 then
    PredioAdm()
  end
  if emanuel == 2 then
    PrefeituraAdm()
  end
  if emanuel == 3 then
    AeroportoAdm()
  end
  if emanuel == 4 then
    Aero2()
  end
  if emanuel == 5 then
    Aero3()
  end
  if emanuel == 6 then
    Aero4()
  end
  if emanuel == 7 then
    Aero5()
  end
  if emanuel == 8 then
    Aero6()
  end
  if emanuel == 9 then
    ExecitoAdm()
  end
  if emanuel == 10 then
    ExecitoAdm2()
  end
end

liberar = off
function TpLocal()
  emanuel = gg.choice({
"🇮🇶متجر أسلحة ",
"🇮🇶التخلص من المركبات ",
"🇮🇶بار ",
"🇮🇶مركز الشرطة ",
"🇮🇶صيدلية ",
"🇮🇶سوق المركبات ",
"🇮🇶متجر ملابس ",
"🇮🇶مستشفى ",
"🇮🇶رصيف ",
"🇮🇶رصيف علوي "
  }, nil, "       ╔══════◄••❀••►══════╗\n       ╠━   『مجاني』 👑  Silk Road 👑 \n       ╚══════◄••❀••►══════╝")
  if emanuel == nil then
    return
  end
  if emanuel == 1 then
    LojaDeArmas()
  end
  if emanuel == 2 then
    DescarteDeVeiculos()
  end
  if emanuel == 3 then
    Buteco()
  end
  if emanuel == 4 then
    Delegacia()
  end
  if emanuel == 5 then
    Farmacia()
  end
  if emanuel == 6 then
    MercadoVeiculos()
  end
  if emanuel == 7 then
    LojaRoupas()
  end
  if emanuel == 8 then
    Hospital()
  end
  if emanuel == 9 then
    Pier()
  end
  if emanuel == 10 then
    PierCima()
  end
end

function Buteco()
  emanuel = gg.choice({
"🇮🇶حاجِز ",
"🇮🇶حاجِز2 "
  }, nil, "       ╔══════◄••❀••►══════╗\n       ╠━   『مجاني』 👑  Silk Road 👑 \n       ╚══════◄••❀••►══════╝")
  if emanuel == nil then
    return
  end
  if emanuel == 1 then
    Bar()
  end
  if emanuel == 2 then
    Bar2()
  end
end

function TpAdm()
  emanuel = gg.choice({
"👑SilkRoad👑المبنى الإداري ",
"👑SilkRoad👑البلدية ",
"👑SilkRoad👑مطار 1 ",
"👑SilkRoad👑مطار 2 ",
"👑SilkRoad👑مطار 3 ",
"👑SilkRoad👑مطار 4 ",
"👑SilkRoad👑مطار 5 ",
"👑SilkRoad👑مطار 6 ",
"👑SilkRoad👑الجيش ",
"👑SilkRoad👑الجيش "
  }, nil, "       ╔══════◄••❀••►══════╗\n       ╠━   『مجاني』 👑  Silk Road  👑 \n       ╚══════◄••❀••►══════╝")
  if emanuel == nil then
    return
  end
  if emanuel == 1 then
    PredioAdm()
  end
  if emanuel == 2 then
    PrefeituraAdm()
  end
  if emanuel == 3 then
    AeroportoAdm()
  end
  if emanuel == 4 then
    Aero2()
  end
  if emanuel == 5 then
    Aero3()
  end
  if emanuel == 6 then
    Aero4()
  end
  if emanuel == 7 then
    Aero5()
  end
  if emanuel == 8 then
    Aero6()
  end
  if emanuel == 9 then
    ExecitoAdm()
  end
  if emanuel == 10 then
    ExecitoAdm2()
  end
end

function NoReload()
  if ori == off then
    X = "WeaponLevelParameters"
    f = "ReloadTime"
    t = 16
    field()
    gg.getResults(9999)
    gg.editAll(0, 16)
    gg.clearResults()
    Enabled_Function()
    ori = on
  else
    X = "WeaponLevelParameters"
    f = "ReloadTime"
    t = 16
    field()
    gg.getResults(9999)
    gg.editAll(3, 16)
    gg.clearResults()
    Disabled_Function()
    ori = off
  end
end

function Boost()
  if oru == off then
    X = "WeaponDamageParameters"
    f = "MinVehicleDamage"
    t = 4
    field()
    local results = gg.getResults(9999)
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(results) do
          _FORV_5_.value = _FORV_5_.value + 20
          _FORV_5_.flags = t
        end
      end
    end
    gg.setValues(results)
    gg.clearResults()
    search("WeaponDamageParameters", 16, true, false, 4)
    local results = gg.getResults(9999)
    t = 4
    do
      do
        for _FORV_5_, _FORV_6_ in ipairs(results) do
          _FORV_6_.value = _FORV_6_.value + 10
          _FORV_6_.flags = t
        end
      end
    end
    gg.setValues(results)
    gg.clearResults()
    Enabled_Function()
    oru = on
  else
    X = "WeaponDamageParameters"
    f = "MinVehicleDamage"
    t = 4
    field()
    local results = gg.getResults(9999)
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(results) do
          _FORV_5_.value = _FORV_5_.value - 20
          _FORV_5_.flags = t
          _FORV_5_.freeze = true
        end
      end
    end
    gg.setValues(results)
    gg.addListItems(results)
    gg.clearResults()
    search("WeaponDamageParameters", "0x10", true, false, 4)
    local results = gg.getResults(9999)
    t = 4
    do
      do
        for _FORV_5_, _FORV_6_ in ipairs(results) do
          _FORV_6_.value = _FORV_6_.value - 10
          _FORV_6_.flags = t
        end
      end
    end
    gg.setValues(results)
    gg.clearResults()
    oru = off
    Disabled_Function()
  end
end

function clear()
  gg.getResults(gg.getResultsCount())
  gg.clearResults()
end

function check()
  E = nil
  E = gg.getResultsCount()
end

function error()
  gg.toast("🥴 خطأ القيمة غير موجودة 🫤")
end

local PontosGrafite = {
  {
    name = "نقطة_2",
    x = 411.8629,
    y = 5.58079147,
    z = 826.7994
  },
  {
    name = "نقطة_8",
    x = 2338.97778,
    y = 20.2885685,
    z = 547.7624
  },
  {
    name = "نقطة_9",
    x = 2357.29175,
    y = 20.43878,
    z = 223.401428
  },
  {
    name = "نقطة_10",
    x = 2603.348,
    y = 20.281189,
    z = 523.842346
  },
  {
    name = "نقطة_11",
    x = 2654.19775,
    y = 20.4662323,
    z = 696.7524
  },
  {
    name = "نقطة_12",
    x = 2794.98584,
    y = 20.257843,
    z = 896.129333
  },
  {
    name = "نقطة_13",
    x = 2788.66479,
    y = 20.2578545,
    z = 1020.21741
  },
  {
    name = "نقطة_14",
    x = 2713.837,
    y = 20.25158,
    z = 1264.98
  },
  {
    name = "نقطة_15",
    x = 2746.16,
    y = 20.21793,
    z = 1431.45
  },
  {
    name = "نقطة_16",
    x = 2863.875,
    y = 20.148653,
    z = 1563.51
  },
  {
    name = "نقطة_17",
    x = 2680.098,
    y = 20.25343,
    z = 1643.42236
  },
  {
    name = "نقطة_18",
    x = 2784.348,
    y = 20.2579765,
    z = 1804.62231
  },
  {
    name = "نقطة_19",
    x = 2850.76782,
    y = 20.2544022,
    z = 1984.85229
  },
  {
    name = "نقطة_20",
    x = 2870.5,
    y = 20.27553,
    z = 2121.29736
  },
  {
    name = "نقطة_21",
    x = 2379.6228,
    y = 20.2613411,
    z = 1885.21
  },
  {
    name = "نقطة_22",
    x = 2377.388,
    y = 20.274065,
    z = 1753.22949
  },
  {
    name = "نقطة_23",
    x = 2607.098,
    y = 20.2552528,
    z = 1113.87231
  },
  {
    name = "نقطة_24",
    x = 2569.87,
    y = 20.2583275,
    z = 930.2233
  },
  {
    name = "نقطة_25",
    x = 1823.88281,
    y = 142.769287,
    z = 2210.46436
  },
  {
    name = "نقطة_26",
    x = 2804.9,
    y = 10.1502457,
    z = 114.891418
  },
  {
    name = "نقطة_27",
    x = 3024.50977,
    y = 10.0001564,
    z = 162.309387
  },
  {
    name = "نقطة_28",
    x = 3042.52,
    y = 10.0002365,
    z = -304.28
  },
  {
    name = "نقطة_29",
    x = 2712.098,
    y = 10.0001736,
    z = -94.00751
  },
  {
    name = "نقطة_30",
    x = 2640.838,
    y = 20.2715549,
    z = 1880.88232
  },
  {
    name = "نقطة_31",
    x = 2523.16772,
    y = 20.2699451,
    z = 2065.48242
  },
  {
    name = "نقطة_32",
    x = 2616.378,
    y = 20.6300774,
    z = 2181.01
  },
  {
    name = "نقطة_34",
    x = 1833.1178,
    y = 20.227169,
    z = 198.100037
  },
  {
    name = "نقطة_37",
    x = 1819.29785,
    y = 20.3093929,
    z = -1063.43774
  },
  {
    name = "نقطة_38",
    x = 1638.44788,
    y = 20.164362,
    z = -873.5976
  },
  {
    name = "نقطة_39",
    x = 1725.08484,
    y = 20.1624184,
    z = -783.2236
  },
  {
    name = "نقطة_40",
    x = 2391.46387,
    y = 25.2468452,
    z = 1039.04
  },
  {
    name = "نقطة_41",
    x = 1301.805,
    y = 24.695,
    z = 1222.665
  },
  {
    name = "نقطة_43",
    x = 1443.761,
    y = 24.75,
    z = 1212.71
  },
  {
    name = "نقطة_44",
    x = 2647.7,
    y = 20.237,
    z = 1703.47
  },
  {
    name = "نقطة_45",
    x = 2581.11,
    y = 20.29,
    z = 1535.99
  },
  {
    name = "نقطة_46",
    x = 2767.08,
    y = 20.26,
    z = 1154.74
  },
  {
    name = "نقطة_48",
    x = 535.21,
    y = 5.47,
    z = 1019.75
  },
  {
    name = "نقطة_49",
    x = 530.762,
    y = 5.61,
    z = 805.163
  },
  {
    name = "نقطة_57",
    x = 562.545,
    y = 32.978,
    z = 1876.514
  },
  {
    name = "نقطة_60",
    x = 3056.98,
    y = 10.155,
    z = 262.62
  },
  {
    name = "نقطة_61",
    x = 2517.935,
    y = 20.143,
    z = 1649.505
  },
  {
    name = "نقطة_63",
    x = 985.922,
    y = 16.762,
    z = 1213.863
  },
  {
    name = "نقطة_65",
    x = 2701.052,
    y = 20.641,
    z = 749.743
  },
  {
    name = "نقطة_66",
    x = 530.846,
    y = 5.6,
    z = 853.467
  },
  {
    name = "نقطة_68",
    x = 420.794,
    y = 5.6,
    z = 1030.22
  },
  {
    name = "نقطة_73",
    x = 1897.774,
    y = 38.09,
    z = 1717.581
  },
  {
    name = "نقطة_74",
    x = 364.577,
    y = 5.5,
    z = 1188.248
  },
  {
    name = "نقطة_75",
    x = 327.343,
    y = 5.607,
    z = 1139.551
  },
  {
    name = "نقطة_77",
    x = 2382.423,
    y = 25.278,
    z = 1324.635
  },
  {
    name = "نقطة_80",
    x = 570.085,
    y = 5.603,
    z = 1123.13
  },
  {
    name = "نقطة_81",
    x = 2960.86,
    y = 10.01,
    z = 283.18
  },
  {
    name = "نقطة_82",
    x = 2037.624,
    y = 31.214,
    z = 1687.566
  },
  {
    name = "نقطة_88",
    x = 2388.39,
    y = 20.29,
    z = 1617.23
  },
  {
    name = "نقطة_89",
    x = 606.54,
    y = 34.07,
    z = 1831.29
  },
  {
    name = "نقطة_94",
    x = 396.977,
    y = 5.6,
    z = 1130.02
  },
  {
    name = "نقطة_96",
    x = 2815.03,
    y = 20.26,
    z = 1044.34
  },
  {
    name = "نقطة_97",
    x = 1992.527,
    y = 38.21,
    z = 1679.3
  },
  {
    name = "نقطة_98",
    x = 2801.128,
    y = 20.26,
    z = 1015.69
  },
  {
    name = "نقطة_104",
    x = 321.61,
    y = 5.601,
    z = 914.93
  },
  {
    name = "نقطة_106",
    x = 486.761,
    y = 5.6,
    z = 1147.64
  },
  {
    name = "نقطة_109",
    x = 2734.39,
    y = 20.265,
    z = 963.52
  },
  {
    name = "نقطة_110",
    x = 1911.469,
    y = 35.13,
    z = 1699.911
  },
  {
    name = "نقطة_113",
    x = 1131.51,
    y = 22.25,
    z = 977.57
  },
  {
    name = "نقطة_114",
    x = 1213.567,
    y = 26.63,
    z = 1062.619
  },
  {
    name = "نقطة_116",
    x = 2777.96,
    y = 20.49,
    z = 712.43
  },
  {
    name = "نقطة_117",
    x = 2528.93,
    y = 20.16,
    z = 1813.85
  },
  {
    name = "نقطة_119",
    x = 1116.22,
    y = 25.89,
    z = 1213.29
  },
  {
    name = "نقطة_120",
    x = 604.081,
    y = 5.42,
    z = 1148.585
  },
  {
    name = "نقطة_121",
    x = 2672.405,
    y = 10.02,
    z = 80.94
  },
  {
    name = "لاعب ضد لاعب_1_1",
    x = 67.46,
    y = 5.661123,
    z = 1175.79
  },
  {
    name = "لاعب ضد لاعب_1_2",
    x = -178.42,
    y = 6.3,
    z = 1095.89
  },
  {
    name = "لاعب ضد لاعب_1_3",
    x = 101.76,
    y = -0.52,
    z = 1771.32
  },
  {
    name = "لاعب ضد لاعب_1_4",
    x = 225.99,
    y = 16.09,
    z = 1459.4
  },
  {
    name = "لاعب ضد لاعب_1_5",
    x = 142.71,
    y = 5.445,
    z = 1700.44
  },
  {
    name = "لاعب ضد لاعب_2_1",
    x = 829.13,
    y = 4.80375338,
    z = 642.7694
  },
  {
    name = "لاعب ضد لاعب_2_2",
    x = 741.324,
    y = 4.832031,
    z = 554.659241
  },
  {
    name = "لاعب ضد لاعب_2_3",
    x = 958.17,
    y = 0.39,
    z = 225.85
  },
  {
    name = "لاعب ضد لاعب_2_4",
    x = 627.152832,
    y = 4.83594,
    z = 257.64
  },
  {
    name = "لاعب ضد لاعب_2_5",
    x = 668.445,
    y = 4.68552,
    z = 392.7
  },
  {
    name = "لاعب ضد لاعب_2_6",
    x = 948.391,
    y = 4.835937,
    z = 430.662
  },
  {
    name = "لاعب ضد لاعب_2_7",
    x = 878.08,
    y = 3.32,
    z = 674.51
  },
  {
    name = "لاعب ضد لاعب_3_1",
    x = 972.19,
    y = 17.8281269,
    z = 951.87
  },
  {
    name = "لاعب ضد لاعب_3_2",
    x = 764.806,
    y = 1.98847,
    z = 786.991
  },
  {
    name = "لاعب ضد لاعب_3_3",
    x = 992.39,
    y = 15.1875,
    z = 897.905
  },
  {
    name = "لاعب ضد لاعب_3_4",
    x = 1014.94,
    y = 2.74658442,
    z = 689.96
  },
  {
    name = "لاعب ضد لاعب_3_5",
    x = 886.73,
    y = 10.968751,
    z = 1053.19751
  },
  {
    name = "لاعب ضد لاعب_3_6",
    x = 883.904,
    y = 5.45312643,
    z = 936.6784
  },
  {
    name = "لاعب ضد لاعب_3_7",
    x = 671.85,
    y = 6.68,
    z = 1153.051
  },
  {
    name = "لاعب ضد لاعب_4_1",
    x = 1480.97632,
    y = 11.9765635,
    z = 264.81
  },
  {
    name = "لاعب ضد لاعب_4_2",
    x = 1498.22,
    y = 10.3828049,
    z = 462.76
  },
  {
    name = "لاعب ضد لاعب_4_3",
    x = 1153.25,
    y = 11.8238792,
    z = 440.94
  },
  {
    name = "لاعب ضد لاعب_4_4",
    x = 1261.778,
    y = 8.000001,
    z = 276.4587
  },
  {
    name = "لاعب ضد لاعب_4_5",
    x = 1086.677,
    y = 5.314863,
    z = 521.873
  },
  {
    name = "لاعب ضد لاعب_5_1",
    x = 1531.7373,
    y = 22.5312614,
    z = 563.34
  },
  {
    name = "لاعب ضد لاعب_5_2",
    x = 1372.43,
    y = 11.5390615,
    z = 511.42157
  },
  {
    name = "لاعب ضد لاعب_5_3",
    x = 1339.878,
    y = 21.77986,
    z = 564.819
  },
  {
    name = "لاعب ضد لاعب_5_4",
    x = 1034.38574,
    y = 14.952733,
    z = 887.935
  },
  {
    name = "لاعب ضد لاعب_5_5",
    x = 1039.607,
    y = 5.91406155,
    z = 747.75
  },
  {
    name = "لاعب ضد لاعب_5_6",
    x = 1260.014,
    y = 20.6944981,
    z = 767.287
  },
  {
    name = "لاعب ضد لاعب_5_7",
    x = 1154.318,
    y = 20.7031269,
    z = 691.62
  },
  {
    name = "لاعب ضد لاعب_6_1",
    x = 1319.84,
    y = 23.7343769,
    z = 740.28
  },
  {
    name = "لاعب ضد لاعب_6_2",
    x = 1578.16772,
    y = 20.2396374,
    z = 876.58
  },
  {
    name = "لاعب ضد لاعب_6_3",
    x = 1364.79,
    y = 22.623579,
    z = 876.058
  },
  {
    name = "لاعب ضد لاعب_6_4",
    x = 1499.99,
    y = 24.4999981,
    z = 1058.325
  },
  {
    name = "لاعب ضد لاعب_6_5",
    x = 1577.45,
    y = 24.5156269,
    z = 993.72
  },
  {
    name = "لاعب ضد لاعب_7_1",
    x = 2032.27,
    y = 29.59375,
    z = 1066.62122
  },
  {
    name = "لاعب ضد لاعب_7_2",
    x = 2046.14807,
    y = 28.5172138,
    z = 917.81
  },
  {
    name = "لاعب ضد لاعب_7_3",
    x = 1780.48,
    y = 23.13,
    z = 800.185
  },
  {
    name = "لاعب ضد لاعب_7_4",
    x = 1737.312,
    y = 23.8593731,
    z = 1176.934
  },
  {
    name = "لاعب ضد لاعب_7_5",
    x = 2040.65,
    y = 24.6927433,
    z = 1197.50269
  },
  {
    name = "لاعب ضد لاعب_7_6",
    x = 1975.88,
    y = 29.4531269,
    z = 1026.2
  },
  {
    name = "لاعب ضد لاعب_7_7",
    x = 1856.166,
    y = 23.2812538,
    z = 816.1
  },
  {
    name = "لاعب ضد لاعب_8_1",
    x = 2063.00879,
    y = 29.2187481,
    z = 1292.968
  },
  {
    name = "لاعب ضد لاعب_8_2",
    x = 2100.65479,
    y = 31.3305283,
    z = 1395.5
  },
  {
    name = "لاعب ضد لاعب_8_3",
    x = 2103.45,
    y = 31.1718769,
    z = 1531.062
  },
  {
    name = "لاعب ضد لاعب_9_1",
    x = 1765.39,
    y = 31.171875,
    z = 1549.68
  },
  {
    name = "لاعب ضد لاعب_9_2",
    x = 1698.97314,
    y = 41.8125,
    z = 1520.62
  },
  {
    name = "لاعب ضد لاعب_9_3",
    x = 1377.01,
    y = 40.3750038,
    z = 1467.54
  },
  {
    name = "لاعب ضد لاعب_9_4",
    x = 1466.88,
    y = 41.8125,
    z = 1515.51
  },
  {
    name = "لاعب ضد لاعب_9_5",
    x = 1576.65,
    y = 41.8125,
    z = 1658.06
  },
  {
    name = "لاعب ضد لاعب_10_1",
    x = 720.75,
    y = 25.2499981,
    z = 1713.23547
  },
  {
    name = "لاعب ضد لاعب_10_2",
    x = 846.97,
    y = 26.67397,
    z = 1371.56384
  },
  {
    name = "لاعب ضد لاعب_10_3",
    x = 947.86,
    y = 25.23482,
    z = 1526.83
  },
  {
    name = "لاعب ضد لاعب_10_4",
    x = 1157.49707,
    y = 44.5937538,
    z = 1501.608
  },
  {
    name = "لاعب ضد لاعب_10_5",
    x = 1215.976,
    y = 40.7187462,
    z = 1389.339
  },
  {
    name = "لاعب ضد لاعب_11_1",
    x = 1021.44,
    y = 47.84375,
    z = 1812.01
  },
  {
    name = "لاعب ضد لاعب_11_2",
    x = 990.95,
    y = 56.2499962,
    z = 1911.71
  },
  {
    name = "لاعب ضد لاعب_11_3",
    x = 1405.64,
    y = 50.54519,
    z = 1826.79
  },
  {
    name = "لاعب ضد لاعب_12_1",
    x = 1658.632,
    y = 50.59375,
    z = 1795.96
  },
  {
    name = "لاعب ضد لاعب_12_2",
    x = 1566.574,
    y = 50.5937538,
    z = 1799.236
  },
  {
    name = "لاعب ضد لاعب_12_3",
    x = 1488.61,
    y = 50.60917,
    z = 1897.372
  },
  {
    name = "حيادي_1",
    x = 1824.81,
    y = 23.3349686,
    z = 753.79
  },
  {
    name = "حيادي_2",
    x = 1703.36,
    y = 23.7677917,
    z = 635.67
  },
  {
    name = "حيادي_3",
    x = 2005.84,
    y = 20.2812462,
    z = 753.608948
  },
  {
    name = "حيادي_4",
    x = 1051.46,
    y = 17.859375,
    z = 1011.7
  },
  {
    name = "حيادي_5",
    x = 942.964,
    y = 16.234375,
    z = 1132.34
  },
  {
    name = "حيادي_6",
    x = 986.98,
    y = 19.6093731,
    z = 1150.59143
  },
  {
    name = "حيادي_7",
    x = 1250.83,
    y = 26.2499981,
    z = 1177.64
  },
  {
    name = "حيادي_8",
    x = 1377.68,
    y = 24.38,
    z = 1157.33
  },
  {
    name = "حيادي_9",
    x = 1421.05,
    y = 24.4843769,
    z = 1122.11
  },
  {
    name = "حيادي_10",
    x = 1775.03,
    y = 24.769165,
    z = 1227.44
  },
  {
    name = "حيادي_11",
    x = 1584.41846,
    y = 24.552393,
    z = 1158.653
  },
  {
    name = "حيادي_12",
    x = 1363.836,
    y = 27.418,
    z = 1267.463
  },
  {
    name = "حيادي_13",
    x = 1168.631,
    y = 26.0468731,
    z = 1237.293
  },
  {
    name = "حيادي_14",
    x = 988.68,
    y = 19.1093845,
    z = 1243.515
  },
  {
    name = "حيادي_15",
    x = 830.215,
    y = 22.0822811,
    z = 1300.493
  },
  {
    name = "حيادي_16",
    x = 1825.021,
    y = 35.2812538,
    z = 1773.232
  },
  {
    name = "حيادي_17",
    x = 1799.21,
    y = 37.347,
    z = 1713.779
  },
  {
    name = "حيادي_18",
    x = 2020.847,
    y = 31.0781269,
    z = 1643.11011
  },
  {
    name = "حيادي_19",
    x = 2090.29,
    y = 28.171875,
    z = 1878.6
  },
  {
    name = "حيادي_20",
    x = 2015.29,
    y = 12.4218731,
    z = 2150.4
  },
  {
    name = "حيادي_21",
    x = 2191.056,
    y = 12.7265615,
    z = 1922.57
  },
  {
    name = "حيادي_22",
    x = 2316.77,
    y = 20.0156269,
    z = 1251.62
  },
  {
    name = "حيادي_23",
    x = 2332.656,
    y = 12.7380419,
    z = 800.542
  },
  {
    name = "حيادي_24",
    x = 344.78,
    y = 32.96875,
    z = 1926.99
  },
  {
    name = "حيادي_25",
    x = 462,
    y = 32.9687576,
    z = 1891.51
  },
  {
    name = "حيادي_26",
    x = 432.41,
    y = 32.96875,
    z = 1822.862
  },
  {
    name = "حيادي_27",
    x = 594.51,
    y = 32.96875,
    z = 1932.96
  },
  {
    name = "حيادي_28",
    x = 708.02,
    y = 37.09375,
    z = 1814.95
  },
  {
    name = "حيادي_29",
    x = 849.26,
    y = 42.90625,
    z = 1895.22
  },
  {
    name = "حيادي_30",
    x = 922.878,
    y = 45.9062538,
    z = 1801.65
  }
}
function ToLoc(coord)
  gg.toast("النقل : " .. coord.name)
  TpLoc(coord.x, coord.y, coord.z)
end

function MenuPontos()
  local nomes = {}
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(PontosGrafite) do
        table.insert(nomes, _FORV_5_.name)
      end
    end
  end
  local escolha = gg.choice(nomes, nil, "『مجاني👑Silk Road  👑")
  if escolha then
    gg.setVisible(false)
    ToLoc(PontosGrafite[escolha])
  end
end

function ExercitoRota1()
  TpLoc("579.7313", "144.683121", "3302.67871")
  TpLoc("632.057861", "146.871414", "3327.968")
  TpLoc("657.9878", "161.561646", "3286.66138")
  TpLoc("683.9673", "166.12056", "3238.046")
  TpLoc("730.615967", "172.50563", "3247.70044")
  TpLoc("775.0398", "172.505615", "3281.62769")
  TpLoc("839.277344", "172.3981", "3241.19165")
end

function ExercitoRota2()
  TpLoc("666.902954", "166.11908", "3247.36768")
  TpLoc("673.317749", "159.833954", "3292.14624")
  TpLoc("647.5237", "149.89386", "3337.77466")
  TpLoc("593.7339", "144.683167", "3342.896")
  TpLoc("568.028931", "144.68309", "3306.82056")
  TpLoc("518.7009", "144.832321", "3352.09277")
  TpLoc("589.483643", "144.8332", "3408.465")
end

function ExercitoRota3()
  TpLoc("771.02", "172.3556", "3194.93726")
  TpLoc("730.2605", "172.505646", "3182.52319")
  TpLoc("709.1644", "172.505615", "3132.88037")
  TpLoc("694.7849", "172.505676", "3079.984")
  TpLoc("694.954956", "173.4703", "3023.164")
  TpLoc("649.5443", "186.384338", "2967.96948")
  TpLoc("648.275146", "182.598648", "2994.04443")
  TpLoc("683.1343", "172.505676", "3069.30518")
end

function ExercitoRota4()
  TpLoc("634.7888", "186.619217", "2976.066")
  TpLoc("681.07605", "173.999313", "3025.53662")
  TpLoc("687.140259", "172.5056", "3118.4292")
  TpLoc("729.958252", "172.50563", "3168.52783")
  TpLoc("797.192261", "172.505585", "3195.49341")
  TpLoc("834.69165", "172.4364", "3228.75684")
  TpLoc("827.768555", "172.5056", "3278.50439")
  TpLoc("749.1852", "172.505615", "3279.732")
end

function LojaDeArmas()
  TpLoc("1845.37145996094", "26.31966590881", "1100.08386230469")
end

function DescarteDeVeiculos()
  TpLoc("1420.427734375", "45.24946594238", "1520.89477539062")
end

function Bar()
  TpLoc("609.18585205078", "33.61267089844", "1874.91052246094")
end

function Bar2()
  TpLoc("639.18585205078", "34.61267089844", "1879.91052246094")
end

function Delegacia()
  TpLoc("1150.96264648438", "38.2646484375", "1100.47045898438")
end

function Farmacia()
  TpLoc("517.00158691406", "5.45533657074", "981.41516113281")
end

function Execito()
  TpLoc("750.51443481445", "280.45437431335", "3170.79675292969")
end

function ExecitoAdm()
  TpLoc("1350.51443481445", "190.45437431335", "3370.79675292969")
end

function ExecitoAdm3()
  TpLoc("1350.51443481445", "220.45437431335", "370.79675292969")
end

function ExecitoAdm4()
  TpLoc("1350.51443481445", "220.45437431335", "3370.79675292969")
end

function ExecitoAdm2()
  TpLoc("1275.51443481445", "200.45437431335", "2930.79675292969")
end

function MercadoVeiculos()
  TpLoc("2800.93518066406", "40.26054191589", "1000.55908203125")
end

function LojaRoupas()
  TpLoc("900.87", "8.98", "827.33")
end

function Hospital()
  TpLoc("1919.175", "30.84", "1368.54")
end

function Pier()
  TpLoc("-460.25024414062", "25.26000022888", "1165.54956054688")
end

function PierCima()
  TpLoc("-440.25024414062", "15.2661781311", "1170.54956054688")
end

function AeroportoAdm()
  TpLoc("1850.11328125", "55.28401756287", "-1500.63342285156")
end

function Aero2()
  TpLoc("1640.11328125", "55.2840175628", "-950.63342285156")
end

function Aero5()
  TpLoc("1790.11328125", "55.2840175628", "-950.63342285156")
end

function Aero6()
  TpLoc("1780.11328125", "140.2840175628", "-1120.63342285156")
end

function Aero4()
  TpLoc("1540.11328125", "80.2840175628", "-900.63342285156")
end

function Aero3()
  TpLoc("1650.11328125", "55.28401756287", "-1500.63342285156")
end

function PredioAdm()
  TpLoc("1503.4599609375", "350.30752944946", "820.50927734375")
end

function PrefeituraAdm()
  TpLoc("1403.4599609375", "140.30752944946", "1020.50927734375")
end

function LojaDeArmas2()
  TpLoc("2050.00604", "371.08777", "2835.972351")
end

function Hp2()
  TpLoc("1918.18585205078", "45.61267089844", "1371.91052246094")
end

function teste()
  TpLoc("493.999481", "244.155426", "2895.792")
end

function CarLojaDeArmas()
  TpCar("1845.37145996094", "26.31966590881", "1100.08386230469")
end

function CarDescarteDeVeiculos()
  TpCar("1420.427734375", "45.24946594238", "1520.89477539062")
end

function CarBar()
  TpCar("609.18585205078", "33.61267089844", "1874.91052246094")
end

function CarBar2()
  TpCar("639.18585205078", "34.61267089844", "1879.91052246094")
end

function CarDelegacia()
  TpCar("1150.96264648438", "38.2646484375", "1100.47045898438")
end

function CarFarmacia()
  TpCar("517.00158691406", "5.45533657074", "981.41516113281")
end

function CarExecito()
  TpCar("750.51443481445", "280.45437431335", "3170.79675292969")
end

function CarExecitoAdm()
  TpCar("1350.51443481445", "190.45437431335", "3370.79675292969")
end

function CarExecitoAdm3()
  TpCar("1350.51443481445", "220.45437431335", "370.79675292969")
end

function CarExecitoAdm4()
  TpCar("1350.51443481445", "220.45437431335", "3370.79675292969")
end

function CarExecitoAdm2()
  TpCar("1275.51443481445", "200.45437431335", "2930.79675292969")
end

function CarMercadoVeiculos()
  TpCar("2800.93518066406", "40.26054191589", "1000.55908203125")
end

function CarLojaRoupas()
  TpCar("900.87", "8.98", "827.33")
end

function CarHospital()
  TpCar("1919.175", "30.84", "1368.54")
end

function CarPier()
  TpCar("-460.25024414062", "25.26000022888", "1165.54956054688")
end

function CarPierCima()
  TpCar("-440.25024414062", "15.2661781311", "1170.54956054688")
end

function CarAeroportoAdm()
  TpCar("1850.11328125", "55.28401756287", "-1500.63342285156")
end

function CarAero2()
  TpCar("1640.11328125", "55.2840175628", "-950.63342285156")
end

function CarAero5()
  TpCar("1790.11328125", "55.2840175628", "-950.63342285156")
end

function CarAero6()
  TpCar("1780.11328125", "140.2840175628", "-1120.63342285156")
end

function CarAero4()
  TpCar("1540.11328125", "80.2840175628", "-900.63342285156")
end

function CarAero3()
  TpCar("1650.11328125", "55.28401756287", "-1500.63342285156")
end

function CarPredioAdm()
  TpCar("1503.4599609375", "350.30752944946", "820.50927734375")
end

function CarPrefeituraAdm()
  TpCar("1403.4599609375", "140.30752944946", "1020.50927734375")
end

function CarLojaDeArmas2()
  TpCar("2050.00604", "371.08777", "2835.972351")
end

function CarHp2()
  TpCar("1918.18585205078", "45.61267089844", "1371.91052246094")
end

function ModoCabecao()
  if um == off then
    gg.clearResults()
    gg.clearList()
    gg.setRanges(32)
    gg.searchNumber("h FD FF 7F 3F F9 FF 7F 3F F5 FF 7F 3F", 1)
    gg.getResults(10000)
    gg.editAll("h FC FF 9F 40 FF FF 9F 40 FF FF 9F 40", 1)
    Enabled_Function()
    um = on
  else
    gg.clearResults()
    gg.clearList()
    gg.setRanges(32)
    gg.searchNumber("h FC FF 9F 40 FF FF 9F 40 FF FF 9F 40", 1)
    gg.getResults(10000)
    gg.editAll("h FD FF 7F 3F F9 FF 7F 3F F5 FF 7F 3F", 1)
    Disabled_Function()
    um = off
  end
end

function BonecoMiniatura()
  gg.setVisible(false)
  gg.clearResults()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.searchNumber("h 00 00 80 3F D7 A3 70 3F D7 A3 70 3F D7 A3 70 3F", gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
  gg.refineNumber("h 00 00 80 3F", gg.TYPE_BYTE)
  gg.sleep(100)
  gg.refineNumber("63", gg.TYPE_BYTE)
  local results = gg.getResults(999)
  if #results == 0 then
    gg.alert("لم يتم العثور على نتائج!")
    return
  end
  R = gg.prompt({
    "🧍 حدد الحجم 👨\n➖➖➖➖➖➖➖➖➖➖ [1036831949 ; 1065353216]"
  }, {
    [1] = defaultValue
  }, {
    [1] = "number"
  })
  if R == nil then
    gg.toast("تم الإلغاء")
    return
  end
  manuelsilvaNO(47, 4)
  manuelsilvaNO(43, 4)
  manuelsilvaNO(39, 4)
  gg.loadResults(gg.getListItems())
  gg.getResults(999)
  gg.editAll(R[1], 4)
  gg.clearResults()
  Enabled_Function()
end

function BonecoGigante()
  gg.setVisible(false)
  gg.clearResults()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.searchNumber("h 00 00 80 3F D7 A3 70 3F D7 A3 70 3F D7 A3 70 3F", gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
  gg.refineNumber("h 00 00 80 3F", gg.TYPE_BYTE)
  gg.sleep(100)
  gg.refineNumber("63", gg.TYPE_BYTE)
  local results = gg.getResults(999)
  if #results == 0 then
    gg.alert("لم يتم العثور على نتائج!")
    return
  end
  R = gg.prompt({
    "🧍 حدد الحجم 👨\n➖➖➖➖➖➖➖➖➖➖ [1 ; 8]"
  }, {
    [1] = defaultValue
  }, {
    [1] = "number"
  })
  if R == nil then
    gg.toast("تم الإلغاء")
    return
  end
  manuelsilvaN(47)
  manuelsilvaN(43)
  manuelsilvaN(39)
  gg.loadResults(gg.getListItems())
  gg.getResults(999)
  gg.editAll(R[1], 16)
  gg.clearResults()
  Enabled_Function()
end

function Collision()
  if cinco == off then
    gg.clearResults()
    gg.clearList()
    AA = "CollisionProxy"
    BB = "OnCollisionEnter"
    o()
    local t = gg.getResults(1)
    local p = {}
    p[1] = {}
    p[1].address = t[1].address + 0
    p[1].flags = 4
    p[1].value = "D65F03C0h"
    gg.addListItems(p)
    gg.loadResults(gg.getListItems())
    gg.setValues(p)
    gg.clearResults()
    gg.clearList()
    Enabled_Function()
    cinco = on
  else
    gg.clearResults()
    gg.clearList()
    AA = "CollisionProxy"
    BB = "OnCollisionEnter"
    o()
    local t = gg.getResults(1)
    local p = {}
    p[1] = {}
    p[1].address = t[1].address + 0
    p[1].flags = 4
    p[1].value = "F9401008h"
    gg.addListItems(p)
    gg.loadResults(gg.getListItems())
    gg.setValues(p)
    gg.clearResults()
    gg.clearList()
    Disabled_Function()
    cinco = off
  end
end

function Gasolina()
  if quatro == off then
    gg.clearResults()
    gg.clearList()
    CreateHook(6329924, 6330160)
    CreateHook(6330724, 6331320)
    CreateHook(6329400, 6329916)
    Enabled_Function()
    quatro = on
  else
    gg.clearResults()
    gg.clearList()
    Disabled_Function()
    quatro = on
  end
end

function prisao()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("1.1", 16)
  gg.refineNumber("1.1", 16)
  local t = gg.getResults(1000)
  if #t == 0 then
    gg.alert("لم يتم العثور على نتائج!")
    os.exit()
  end
  if #t > 500 then
    local newT = {}
    do
      do
        for _FORV_5_ = 501, #t do
          table.insert(newT, t[_FORV_5_])
        end
      end
    end
    t = newT
  end
  gg.loadResults(t)
  local final = gg.getResults(gg.getResultsCount())
  gg.editAll(999999, 16)
  gg.sleep(1000)
  gg.editAll(1.1, 16)
  gg.clearResults()
  gg.clearList()
  seis = off
end

function Stamina()
  if tres == off then
    gg.clearResults()
    gg.clearList()
    AA = "PedViewStorage"
    BB = "SetStaminaLose"
    o()
    local t = gg.getResults(1)
    local p = {}
    p[1] = {}
    p[1].address = t[1].address + 0
    p[1].flags = 4
    p[1].value = "D65F03C0h"
    gg.addListItems(p)
    gg.loadResults(gg.getListItems())
    gg.setValues(p)
    gg.clearResults()
    gg.clearList()
    Enabled_Function()
    tres = on
  else
    gg.clearResults()
    gg.clearList()
    AA = "PedViewStorage"
    BB = "SetStaminaLose"
    o()
    local t = gg.getResults(1)
    local p = {}
    p[1] = {}
    p[1].address = t[1].address + 0
    p[1].flags = 4
    p[1].value = "D10103FFh"
    gg.setValues(p)
    gg.clearResults()
    gg.clearList()
    Disabled_Function()
    tres = off
  end
end

function Speed()
  gg.setRanges(gg.REGION_C_DATA)
  gg.clearResults()
  gg.clearList()
  gg.searchNumber("-400107883", 4)
  local r = gg.getResults(gg.getResultsCount())
  gg.clearResults()
  gg.clearList()
  gg.sleep(400)
  R = gg.prompt({
    "🕖 حدد السرعة 🕖\n➖➖➖➖➖➖➖➖➖➖ [1041313291; 1045313291]"
  }, {
    [1] = defaultValue
  }, {
    [1] = "number"
  })
  if R == nil then
    gg.toast("تم الإلغاء")
    return
  end
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(r) do
        _FORV_5_.address = _FORV_5_.address + 4
        _FORV_5_.flags = 4
      end
    end
  end
  gg.loadResults(r)
  gg.getResults(gg.getResultsCount())
  gg.editAll(R[1], 4)
  Enabled_Function()
end

function Base()
  if liberar == off then
    gg.clearResults()
    search("CharacterActor", "0x4C", true, false, 16)
    local resultsX = gg.getResults(500)
    addressesX = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(resultsX) do
          local address = string.format("%x", _FORV_5_.address)
          table.insert(addressesX, {
            name = "X_" .. _FORV_4_,
            address = tonumber(address, 16),
            flags = gg.TYPE_FLOAT
          })
        end
      end
    end
    addressesY = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesX) do
          local address_address = string.format("%x", _FORV_5_.address)
          local new_address = tonumber(address_address, 16) + 4
          table.insert(addressesY, {
            name = "Y_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    addressesZ = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesX) do
          local address_address = string.format("%x", _FORV_5_.address)
          local new_address = tonumber(address_address, 16) + 8
          table.insert(addressesZ, {
            name = "Z_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    liberar = on
    gg.alert("تم إصدار Tp🔓")
  else
    gg.alert("تم إصدار Tp🔓")
  end
end

function TpCarMarker()
  sapo = gg.multiChoice({
"🇮🇶فتح علامة Tp 🔓",
"🇮🇶مركبة النقل الآني إلى النقطة ➡️",
"🇮🇶تحديد موقع السيارة 🚗"
  }, nil, "『مجاني』 👑   لا تنسون الاشتراك بقناه سلك رودSilk Road  👑📍\n")
  if sapo == nil then
    return
  end
  if sapo[1] then
    Unlock()
  end
  if sapo[2] then
    GoTp()
  end
  if sapo[3] then
    UpdateID()
  end
end

function TpGo()
  if tiado ~= 1 then
    gg.alert("علامة مجانية أو Tp")
    return
  end
  local searchString = coordinatesToSearchString(Co_X, Co_Y, Co_Z)
  gg.clearResults()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.searchNumber(searchString, gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
  local results = gg.getResults(3000)
  if #results < 3 then
    gg.alert("لم يتم العثور على إحداثيات النقطة.")
    return
  end
  local allPoints = {}
  do
    do
      for _FORV_6_ = 1, #results - 2, 3 do
        local addrX = results[_FORV_6_].address
        local addrY = results[_FORV_6_ + 1].address
        local addrZ = results[_FORV_6_ + 2].address
        if addrY - addrX == 4 and addrZ - addrY == 4 then
          table.insert(allPoints, {
            x = addrX,
            y = addrY,
            z = addrZ
          })
        end
      end
    end
  end
  gg.getResults(3000)
  UpdateCoordinates()
  local carX = VehicleCoordinates.x
  local carY = VehicleCoordinates.y
  local carZ = VehicleCoordinates.z
  local setList = {}
  do
    do
      for _FORV_10_, _FORV_11_ in ipairs(allPoints) do
        table.insert(setList, {
          address = _FORV_11_.x,
          flags = gg.TYPE_FLOAT,
          value = carX
        })
        table.insert(setList, {
          address = _FORV_11_.y,
          flags = gg.TYPE_FLOAT,
          value = carY
        })
        table.insert(setList, {
          address = _FORV_11_.z,
          flags = gg.TYPE_FLOAT,
          value = carZ
        })
      end
    end
  end
  gg.setValues(setList)
  gg.toast("تم نقل جميع نقاط المطابقة إلى السيارة!")
end

function floatToHex(value)
  if value == nil then
    return nil
  end
  local packed = string.pack("<f", value)
  local hex = ""
  do
    do
      for _FORV_6_ = 1, #packed do
        hex = hex .. string.format("%02X ", packed:byte(_FORV_6_))
      end
    end
  end
  return hex:sub(1, -2)
end

function coordinatesToSearchString(x, y, z)
  return "h " .. floatToHex(x) .. " " .. floatToHex(y) .. " " .. floatToHex(z)
end

function GoTp()
  if tiado == 1 then
    UpdateCoordinates()
    local results = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesX) do
          local item = {
            address = _FORV_5_.address,
            flags = gg.TYPE_FLOAT,
            value = CurrentCoordinates.x
          }
          gg.setValues({item})
          table.insert(results, item)
        end
      end
    end
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesY) do
          local item = {
            address = _FORV_5_.address,
            flags = gg.TYPE_FLOAT,
            value = CurrentCoordinates.y + 4
          }
          gg.setValues({item})
          table.insert(results, item)
        end
      end
    end
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesZ) do
          local item = {
            address = _FORV_5_.address,
            flags = gg.TYPE_FLOAT,
            value = CurrentCoordinates.z
          }
          gg.setValues({item})
          table.insert(results, item)
        end
      end
    end
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(results) do
          _FORV_5_.freeze = true
        end
      end
    end
    gg.addListItems(results)
    gg.sleep(1000)
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(results) do
          _FORV_5_.freeze = false
        end
      end
    end
    gg.addListItems(results)
  else
    gg.alert("علامة مجانية أو Tp")
  end
end

function UpdateID()
  if tiado == 1 then
    SearchTpCar = "h AE C5 9D 74 0A D7 23 3C CD CC 4C 3D"
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber(SearchTpCar, 1)
    gg.refineNumber("-82", 1)
    t = {}
    t = gg.getResults(1000)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(t) do
          _FORV_4_.address = _FORV_4_.address + 92
          _FORV_4_.flags = 16
        end
      end
    end
    gg.addListItems(t)
    gg.loadResults(gg.getListItems(t))
    local resultsX = gg.getResults(500)
    addressesX = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(resultsX) do
          local address = string.format("%x", _FORV_5_.address)
          table.insert(addressesX, {
            name = "X_" .. _FORV_4_,
            address = tonumber(address, 16),
            flags = gg.TYPE_FLOAT
          })
        end
      end
    end
    addressesY = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesX) do
          local address_address = string.format("%x", _FORV_5_.address)
          local new_address = tonumber(address_address, 16) + 4
          table.insert(addressesY, {
            name = "Y_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    addressesZ = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(addressesX) do
          local address_address = string.format("%x", _FORV_5_.address)
          local new_address = tonumber(address_address, 16) + 8
          table.insert(addressesZ, {
            name = "Z_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    gg.clearList()
    gg.clearResults()
    gg.alert("تم تحديد موقع المركبة وهي جاهزة للنقل  ✅️")
  else
    gg.alert("علامة مجانية أو Tp")
  end
end

function Unlock()
  if tiado == 1 then
    gg.clearResults()
    gg.alert("لقد تم تفعيله بالفعل ✅️")
  else
    gg.alert("‼️انتباه ‼️\n\n1. ادخل إلى السيارة\n2. حدد النقطة على الخريطة\n")
    gg.clearResults()
    gg.setRanges(32)
    search("NavNode", "0x10", true, false, 16)
    gg.getResults(gg.getResultsCount())
    local resultsX = gg.getResults(500)
    if #resultsX == 0 then
      gg.alert("❗️يبدو أنك لم تحدد نقطة على الخريطة ❗️")
      do return Home() end
      return
    end
    COaddressesX = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(resultsX) do
          local new_address = _FORV_5_.address
          table.insert(COaddressesX, {
            name = "CO_X_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    COaddressesY = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(COaddressesX) do
          local new_address = _FORV_5_.address + 4
          table.insert(COaddressesY, {
            name = "CO_Y_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    COaddressesZ = {}
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(COaddressesX) do
          local new_address = _FORV_5_.address + 8
          table.insert(COaddressesZ, {
            name = "CO_Z_" .. _FORV_4_,
            address = new_address
          })
        end
      end
    end
    gg.clearResults()
    gg.clearList()
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(COaddressesX) do
          Co_X = gg.getValues({
            {
              address = _FORV_5_.address,
              flags = gg.TYPE_FLOAT
            }
          })[1].value
        end
      end
    end
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(COaddressesY) do
          Co_Y = gg.getValues({
            {
              address = _FORV_5_.address,
              flags = gg.TYPE_FLOAT
            }
          })[1].value
        end
      end
    end
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(COaddressesZ) do
          Co_Z = gg.getValues({
            {
              address = _FORV_5_.address,
              flags = gg.TYPE_FLOAT
            }
          })[1].value
        end
      end
    end
    CurrentCoordinates = {
      x = 0,
      y = 0,
      z = 0
    }
    function UpdateCoordinates()
      do
        do
          for _FORV_3_, _FORV_4_ in ipairs(COaddressesX) do
            CurrentCoordinates.x = gg.getValues({
              {
                address = _FORV_4_.address,
                flags = gg.TYPE_FLOAT
              }
            })[1].value
          end
        end
      end
      do
        do
          for _FORV_3_, _FORV_4_ in ipairs(COaddressesY) do
            CurrentCoordinates.y = gg.getValues({
              {
                address = _FORV_4_.address,
                flags = gg.TYPE_FLOAT
              }
            })[1].value
          end
        end
      end
      do
        do
          for _FORV_3_, _FORV_4_ in ipairs(COaddressesZ) do
            CurrentCoordinates.z = gg.getValues({
              {
                address = _FORV_4_.address,
                flags = gg.TYPE_FLOAT
              }
            })[1].value
          end
        end
      end
      do
        do
          for _FORV_3_, _FORV_4_ in ipairs(addressesX) do
            VehicleCoordinatesX = gg.getValues({
              {
                address = _FORV_4_.address,
                flags = gg.TYPE_FLOAT
              }
            })[1].value
          end
        end
      end
      do
        do
          for _FORV_3_, _FORV_4_ in ipairs(addressesY) do
            VehicleCoordinatesY = gg.getValues({
              {
                address = _FORV_4_.address,
                flags = gg.TYPE_FLOAT
              }
            })[1].value
          end
        end
      end
      do
        do
          for _FORV_3_, _FORV_4_ in ipairs(addressesZ) do
            VehicleCoordinatesZ = gg.getValues({
              {
                address = _FORV_4_.address,
                flags = gg.TYPE_FLOAT
              }
            })[1].value
          end
        end
      end
      VehicleCoordinates = {
        x = VehicleCoordinatesX,
        y = VehicleCoordinatesY,
        z = VehicleCoordinatesZ
      }
    end
    
    SearchTpCar = "h AE C5 9D 74 0A D7 23 3C CD CC 4C 3D"
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber(SearchTpCar, 1)
    gg.refineNumber("-82", 1)
    t = {}
    t = gg.getResults(1000)
    do
      do
        for _FORV_4_, _FORV_5_ in ipairs(t) do
          _FORV_5_.address = _FORV_5_.address + 92
          _FORV_5_.flags = 16
        end
      end
    end
    gg.addListItems(t)
    gg.loadResults(gg.getListItems(t))
    local resultsX = gg.getResults(500)
    addressesX = {}
    do
      do
        for _FORV_5_, _FORV_6_ in ipairs(resultsX) do
          local address = string.format("%x", _FORV_6_.address)
          table.insert(addressesX, {
            name = "X_" .. _FORV_5_,
            address = tonumber(address, 16),
            flags = gg.TYPE_FLOAT
          })
        end
      end
    end
    addressesY = {}
    do
      do
        for _FORV_5_, _FORV_6_ in ipairs(addressesX) do
          local address_address = string.format("%x", _FORV_6_.address)
          local new_address = tonumber(address_address, 16) + 4
          table.insert(addressesY, {
            name = "Y_" .. _FORV_5_,
            address = new_address
          })
        end
      end
    end
    addressesZ = {}
    do
      do
        for _FORV_5_, _FORV_6_ in ipairs(addressesX) do
          local address_address = string.format("%x", _FORV_6_.address)
          local new_address = tonumber(address_address, 16) + 8
          table.insert(addressesZ, {
            name = "Z_" .. _FORV_5_,
            address = new_address
          })
        end
      end
    end
    tiado = 1
    gg.alert("Tp Marker Liberado")
  end
end

function WallHack()
  if oito == off then
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber("h 6F 12 83 3A AE C5 9D 74 0A D7 A3 3B 0A D7 23 3B", 1)
    gg.refineNumber("111", 1)
    sleep = gg.getResults(100)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(sleep) do
          _FORV_4_.address = _FORV_4_.address - 48
          _FORV_4_.flags = gg.TYPE_FLOAT
          _FORV_4_.value = "20"
        end
      end
    end
    gg.setValues(sleep)
    Enabled_Function()
    oito = on
  else
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber("h 6F 12 83 3A AE C5 9D 74 0A D7 A3 3B 0A D7 23 3B", 1)
    gg.refineNumber("111", 1)
    sleep = gg.getResults(100)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(sleep) do
          _FORV_4_.address = _FORV_4_.address - 48
          _FORV_4_.flags = gg.TYPE_FLOAT
          _FORV_4_.value = "-10"
        end
      end
    end
    gg.setValues(sleep)
    Disabled_Function()
    oito = off
  end
end

function Velocidade()
  if sete == off then
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber("h 6F 12 83 3A AE C5 9D 74 0A D7 A3 3B 0A D7 23 3B", 1)
    gg.refineNumber("111", 1)
    sleep = gg.getResults(100)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(sleep) do
          _FORV_4_.address = _FORV_4_.address - 20
          _FORV_4_.flags = gg.TYPE_FLOAT
          _FORV_4_.value = "-0.1"
        end
      end
    end
    gg.setValues(sleep)
    Enabled_Function()
    sete = on
  else
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber("h 6F 12 83 3A AE C5 9D 74 0A D7 A3 3B 0A D7 23 3B", 1)
    gg.refineNumber("111", 1)
    sleep = gg.getResults(100)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(sleep) do
          _FORV_4_.address = _FORV_4_.address - 20
          _FORV_4_.flags = gg.TYPE_FLOAT
          _FORV_4_.value = "0.1"
        end
      end
    end
    gg.setValues(sleep)
    Disabled_Function()
    sete = off
  end
end

function Morte()
  if seis == off then
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber("h 6F 12 83 3A AE C5 9D 74 0A D7 A3 3B 0A D7 23 3B", 1)
    gg.refineNumber("111", 1)
    sleep = gg.getResults(100)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(sleep) do
          _FORV_4_.address = _FORV_4_.address - 24
          _FORV_4_.flags = gg.TYPE_FLOAT
          _FORV_4_.value = "-1"
        end
      end
    end
    gg.setValues(sleep)
    Enabled_Function()
    seis = on
  else
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber("h 6F 12 83 3A AE C5 9D 74 0A D7 A3 3B 0A D7 23 3B", 1)
    gg.refineNumber("111", 1)
    sleep = gg.getResults(100)
    do
      do
        for _FORV_3_, _FORV_4_ in ipairs(sleep) do
          _FORV_4_.address = _FORV_4_.address - 24
          _FORV_4_.flags = gg.TYPE_FLOAT
          _FORV_4_.value = "0.1"
        end
      end
    end
    gg.setValues(sleep)
    Disabled_Function()
    seis = off
  end
end

function TpCarMarkerGo(X, Y, Z)
  do
    do
      for _FORV_6_, _FORV_7_ in ipairs(addressesX) do
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = X
          }
        })
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = X
          }
        })
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = X
          }
        })
      end
    end
  end
  do
    do
      for _FORV_6_, _FORV_7_ in ipairs(addressesY) do
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = Y
          }
        })
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = Y
          }
        })
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = Y
          }
        })
      end
    end
  end
  do
    do
      for _FORV_6_, _FORV_7_ in ipairs(addressesZ) do
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = Z
          }
        })
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = Z
          }
        })
        gg.setValues({
          {
            address = _FORV_7_.address,
            flags = gg.TYPE_FLOAT,
            value = Z
          }
        })
      end
    end
  end
end

function o()
  local ti = gg.getTargetInfo()
  local p_size = ti.x64 and 8 or 4
  local getvalue = function(address, ggType)
    return gg.getValues({
      {address = address, flags = ggType}
    })[1].value
  end
  
  local ptr = function(address)
    return getvalue(address, ti.x64 and gg.TYPE_QWORD or gg.TYPE_DWORD)
  end
  
  local CString = function(address, str)
    local bytes = gg.bytes(str)
    do
      do
        for _FORV_6_ = 1, #bytes do
          if getvalue(address + _FORV_6_ - 1, gg.TYPE_BYTE) & 255 ~= bytes[_FORV_6_] then
            return false
          end
        end
      end
    end
    return getvalue(address + #bytes, gg.TYPE_BYTE) == 0
  end
  
  local GetIl2CppMethod = function(clazz, method)
    local result = {}
    gg.clearResults()
    gg.setRanges(gg.REGION_C_ALLOC | gg.REGION_C_DATA | gg.REGION_C_BSS | gg.REGION_ANONYMOUS | gg.REGION_OTHER)
    gg.searchNumber(string.format("Q'%s' ", method), gg.TYPE_BYTE)
    local count = gg.getResultsCount()
    if count ~= 0 then
      gg.refineNumber(method:byte(), gg.TYPE_BYTE)
      local t = gg.getResults(count)
      gg.setRanges(gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
      gg.loadResults(t)
      gg.searchPointer(0)
      t = gg.getResults(count)
      do
        do
          for _FORV_8_, _FORV_9_ in ipairs(t) do
            if CString(ptr(ptr(_FORV_9_.address + p_size) + p_size * 2), clazz) then
              table.insert(result, {
                address = ptr(_FORV_9_.address - p_size * 2),
                name = string.format("%s : %s", clazz, method),
                flags = 4
              })
            end
          end
        end
      end
      gg.clearResults()
    end
    return result
  end
  
  K = GetIl2CppMethod(AA, BB)
  gg.loadResults(K)
end

function TpCar(pos_Y, pos_X, pos_Z)
  SearchTpCar = "h AE C5 9D 74 0A D7 23 3C CD CC 4C 3D"
  gg.setRanges(32)
  gg.clearResults()
  gg.searchNumber(SearchTpCar, 1)
  gg.refineNumber("-82", 1)
  TP = gg.getResults(100)
  manuelsilvaP(92)
  manuelsilvaP(96)
  manuelsilvaP(100)
  gg.loadResults(gg.getListItems(t))
  gg.getResults(2000)
  gg.editAll(pos_Y .. ";" .. pos_X .. ";" .. pos_Z, 16)
  local results = gg.getResults(2000)
  do
    do
      for _FORV_7_, _FORV_8_ in ipairs(results) do
        _FORV_8_.freeze = true
      end
    end
  end
  gg.addListItems(results)
  gg.sleep(500)
  do
    do
      for _FORV_7_, _FORV_8_ in ipairs(results) do
        _FORV_8_.freeze = false
      end
    end
  end
  gg.addListItems(results)
  Enabled_Function()
end

function TpLoc(pos_Y, pos_X, pos_Z)
  SearchTp = "h 01 00 01 01 01 00 00 00 01 00 00 00 01 00 00 00"
  gg.setRanges(32)
  gg.clearResults()
  gg.searchNumber(SearchTp, 1)
  gg.refineNumber("1", 1)
  TP = gg.getResults(100)
  manuelsilvaP(44)
  manuelsilvaP(48)
  manuelsilvaP(52)
  gg.loadResults(gg.getListItems(t))
  gg.getResults(2000)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  Enabled_Function()
end

function TpFarm(pos_Y, pos_X, pos_Z)
  gg.loadResults(gg.getListItems())
  TP = gg.getResults(2000)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
  gg.editAll("" .. pos_Y .. ";" .. pos_X .. ";" .. pos_Z .. "", 16)
end

function manuelsilvaNO(address, flags)
  t = {}
  t = gg.getResults(100)
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(t) do
        _FORV_6_.address = _FORV_6_.address - address
        _FORV_6_.flags = flags
      end
    end
  end
  gg.addListItems(t)
end

function manuelsilvaN(address)
  t = {}
  t = gg.getResults(100)
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(t) do
        _FORV_5_.address = _FORV_5_.address - address
        _FORV_5_.flags = 16
      end
    end
  end
  gg.addListItems(t)
end

function manuelsilvaP(address)
  t = {}
  t = gg.getResults(100)
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(t) do
        _FORV_5_.address = _FORV_5_.address + address
        _FORV_5_.flags = 16
      end
    end
  end
  gg.addListItems(t)
end

function Enabled_Function()
  gg.toast("✔️")
end

function Disabled_Function()
  gg.toast("❌")
end

function EXITEX()
  gg.setVisible(true)
  gg.clearResults()
  gg.clearList()
  print("            ")
  print("\n\n✅『مجاني』 👑   Silk Road 👑✅")
  print("------------------------------------------------------")
  print("            ")
  os.exit()
end

function valueFromClass(e, f, g, j, k)
  gg.setVisible(false)
  if j == "32" then
    j = true
  end
  if j == "64" then
    j = false
  end
  Get_user_input = {}
  Get_user_input[1] = e
  Get_user_input[2] = f
  Get_user_input[3] = g
  Get_user_input[4] = j
  Get_user_type = k
  start()
end

function found_(l)
  if error == 1 then
    found2(l)
  elseif error == 2 then
    found3(l)
  elseif error == 3 then
    found4(l)
  else
    found(l)
  end
end

function found(l)
  if count == 0 then
    gg.clearResults()
    gg.clearList()
    first_error = l
    error = 1
    second_start()
  end
end

function found2(l)
  if count == 0 then
    gg.clearResults()
    gg.clearList()
    second_error = l
    error = 2
    third_start()
  end
end

function found3(l)
  if count == 0 then
    gg.clearResults()
    gg.clearList()
    third_error = l
    error = 3
    fourth_start()
  end
end

function found4(l)
  Script_Error = false
  if count == 0 then
    gg.clearResults()
    gg.clearList()
    Script_Error = true
  end
end

function user_input_taker()
  error = 0
end

function O_initial_search()
  gg.setVisible(false)
  user_input = ":" .. Get_user_input[1]
  if Get_user_input[3] then
    offst = 25
  else
    offst = 0
  end
end

function O_dinitial_search()
  if error > 1 then
    gg.setRanges(gg.REGION_C_ALLOC)
  else
    gg.setRanges(gg.REGION_OTHER)
  end
  gg.searchNumber(user_input, gg.TYPE_BYTE)
  count = gg.getResultsCount()
  if count == 0 then
    found_("O_dinitial_search")
    return 0
  end
  Refiner = gg.getResults(1)
  gg.refineNumber(Refiner[1].value, gg.TYPE_BYTE)
  count = gg.getResultsCount()
  if count == 0 then
    found_("O_dinitial_search")
    return 0
  end
  val = gg.getResults(count)
  gg.addListItems(val)
end

function CA_pointer_search()
  gg.clearResults()
  gg.setRanges(gg.REGION_C_ALLOC | gg.REGION_OTHER | 32)
  gg.loadResults(gg.getListItems())
  gg.searchPointer(offst)
  count = gg.getResultsCount()
  if count == 0 then
    found_("CA_pointer_search")
    return 0
  end
  vel = gg.getResults(count)
  gg.clearList()
  gg.addListItems(vel)
end

function CA_apply_offset()
  if Get_user_input[4] then
    tanker = -8
  else
    tanker = -16
  end
  local m = false
  local o = gg.getListItems()
  if not m then
    gg.removeListItems(o)
  end
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(o) do
        _FORV_6_.address = _FORV_6_.address + tanker
        if m then
          _FORV_6_.name = _FORV_6_.name .. " #2"
        end
      end
    end
  end
  gg.addListItems(o)
end

function CA2_apply_offset()
  if Get_user_input[4] then
    tanker = -8
  else
    tanker = -16
  end
  local m = false
  local o = gg.getListItems()
  if not m then
    gg.removeListItems(o)
  end
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(o) do
        _FORV_6_.address = _FORV_6_.address + tanker
        if m then
          _FORV_6_.name = _FORV_6_.name .. " #2"
        end
      end
    end
  end
  gg.addListItems(o)
end

function Q_apply_fix()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.loadResults(gg.getListItems())
  gg.clearList()
  count = gg.getResultsCount()
  if count == 0 then
    found_("Q_apply_fix")
    return 0
  end
  yy = gg.getResults(1000)
  gg.clearResults()
  i = 1
  c = 1
  s = {}
  while i - 1 < count do
    yy[i].address = yy[i].address + -5476377146882523136
    gg.searchNumber(yy[i].address, gg.TYPE_QWORD)
    cnt = gg.getResultsCount()
    if 0 < cnt then
      bytr = gg.getResults(cnt)
      n = 1
      while n - 1 < cnt do
        s[c] = {}
        s[c].address = bytr[n].address
        s[c].flags = 32
        n = n + 1
        c = c + 1
      end
    end
    gg.clearResults()
    i = i + 1
  end
  gg.addListItems(s)
end

function A_base_value()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.loadResults(gg.getListItems())
  gg.clearList()
  gg.searchPointer(offst)
  count = gg.getResultsCount()
  if count == 0 then
    found_("A_base_value")
    return 0
  end
  tel = gg.getResults(count)
  gg.addListItems(tel)
end

function A_base_accuracy()
  gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_ALLOC)
  gg.loadResults(gg.getListItems())
  gg.clearList()
  gg.searchPointer(offst)
  count = gg.getResultsCount()
  if count == 0 then
    found_("A_base_accuracy")
    return 0
  end
  kol = gg.getResults(count)
  i = 1
  h = {}
  while i - 1 < count do
    h[i] = {}
    h[i].address = kol[i].value
    h[i].flags = 32
    i = i + 1
  end
  gg.addListItems(h)
end

function A_user_given_offset()
  local p = gg.getListItems()
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(p) do
        _FORV_5_.address = _FORV_5_.address + Get_user_input[2]
        _FORV_5_.flags = Get_user_type
      end
    end
  end
  gg.clearResults()
  gg.clearList()
  gg.loadResults(p)
  count = gg.getResultsCount()
  if count == 0 then
    found_("Q_apply_fix++")
    return 0
  end
end

function start()
  user_input_taker()
  O_initial_search()
  O_dinitial_search()
  if error > 0 then
    return 0
  end
  CA_pointer_search()
  if error > 0 then
    return 0
  end
  CA_apply_offset()
  if error > 0 then
    return 0
  end
  A_base_value()
  if error > 0 then
    return 0
  end
  if offst == 0 then
    A_base_accuracy()
  end
  if error > 0 then
    return 0
  end
  A_user_given_offset()
  if error > 0 then
    return 0
  end
  if error > 0 then
    return 0
  end
end

function second_start()
  O_dinitial_search()
  if error > 1 then
    return 0
  end
  CA_pointer_search()
  if error > 1 then
    return 0
  end
  CA_apply_offset()
  if error > 1 then
    return 0
  end
  Q_apply_fix()
  if error > 1 then
    return 0
  end
  if offst == 0 then
    A_base_accuracy()
  end
  if error > 1 then
    return 0
  end
  A_user_given_offset()
  if error > 1 then
    return 0
  end
  if error > 1 then
    return 0
  end
end

function third_start()
  O_dinitial_search()
  if error > 2 then
    return 0
  end
  CA_pointer_search()
  if error > 2 then
    return 0
  end
  if offst == 0 then
    CA2_apply_offset()
  end
  if error > 2 then
    return 0
  end
  A_base_value()
  if error > 2 then
    return 0
  end
  if offst == 0 then
    A_base_accuracy()
  end
  if error > 2 then
    return 0
  end
  A_user_given_offset()
  if error > 2 then
    return 0
  end
  if error > 2 then
    return 0
  end
end

function fourth_start()
  O_dinitial_search()
  CA_pointer_search()
  CA2_apply_offset()
  Q_apply_fix()
  if offst == 0 then
    A_base_accuracy()
  end
  A_user_given_offset()
end

GrupoPontoMapa = {}
addressesX = {}
addressesY = {}
addressesZ = {}
function floatToByteArray(value)
  local hex_value = gg.toHex(value, gg.TYPE_FLOAT)
  return {
    hex_value:sub(1, 2),
    hex_value:sub(3, 4),
    hex_value:sub(5, 6),
    hex_value:sub(7, 8)
  }
end

local posVeiculo = {
  x = 0,
  y = 0,
  z = 0
}
function floatToByteArray(value)
  local hex_value = gg.toHex(value, gg.TYPE_FLOAT)
  return {
    hex_value:sub(1, 2),
    hex_value:sub(3, 4),
    hex_value:sub(5, 6),
    hex_value:sub(7, 8)
  }
end

function FarmAll()
  local sapo = gg.multiChoice({
"🇮🇶اختر الموقع ",
"🇮🇶ابدأ المزرعة التلقائية ",
"🇮🇶⬅القائمة الرئيسية "
  }, nil, "『مجاني』 👑  Silk Road 👑\n")
  if sapo == nil then
    return
  end
  if sapo[1] then
    escolherLoc()
  end
  if sapo[2] then
    Ativaro()
  end
  if sapo[3] then
    menu_roubo_ativo = false
    return gg.setVisible(true)
  end
end

function Ativaro()
  gg.alert("‼️ ⚠️ انتبه! أنت بحاجة لأن تكون داخل مركبة 🚙\nانتظر ظهور خط أصفر حتى الوجهة المحددة قبل التفعيل‼️\n\nملاحظة.. تحتاج فقط لتحديد النقطة مرة واحدة")
  gg.clearResults()
  gg.setRanges(32)
  search("NavigationGraph", "0x50", true, false, 16)
  local resultsX = gg.getResults(1)
  if #resultsX == 0 then
    gg.alert("❗️يبدو أنك لم تحدد نقطة على الخريطة ❗️")
    return Home()
  end
  local COaddressesX = {}
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(resultsX) do
        table.insert(COaddressesX, {
          address = _FORV_6_.address
        })
      end
    end
  end
  GrupoPontoMapa = {}
  do
    do
      for _FORV_5_ = 1, #COaddressesX do
        local x = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address,
            flags = gg.TYPE_FLOAT
          }
        })
        local y = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address + 4,
            flags = gg.TYPE_FLOAT
          }
        })
        local z = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address + 8,
            flags = gg.TYPE_FLOAT
          }
        })
        if x[1].value ~= 0 and y[1].value ~= 0 and z[1].value ~= 0 then
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address,
            flags = gg.TYPE_FLOAT,
            value = x[1].value
          })
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address + 4,
            flags = gg.TYPE_FLOAT,
            value = y[1].value
          })
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address + 8,
            flags = gg.TYPE_FLOAT,
            value = z[1].value
          })
        end
      end
    end
  end
  gg.alert("✅")
  if #GrupoPontoMapa == 0 then
    gg.alert("❗️غير قادر على التقاط إحداثيات النقاط على الخريطة.")
    return Home()
  end
  if not posVeiculo or posVeiculo.x == 0 and posVeiculo.y == 0 and posVeiculo.z == 0 then
    gg.alert("❗️لم يتم التقاط موقع المركبة أو أنه غير صحيح. تأكد من وجودك داخل المركبة..")
    return Home()
  end
  local xAnterior, yAnterior, zAnterior
  repeat
    local valoresAtualizados = gg.getValues({
      {
        address = GrupoPontoMapa[1].address,
        flags = gg.TYPE_FLOAT
      },
      {
        address = GrupoPontoMapa[2].address,
        flags = gg.TYPE_FLOAT
      },
      {
        address = GrupoPontoMapa[3].address,
        flags = gg.TYPE_FLOAT
      }
    })
    local x = valoresAtualizados[1].value
    local y = valoresAtualizados[2].value
    local z = valoresAtualizados[3].value
    xAnterior, yAnterior, zAnterior = x, y, z
    local bytesX = floatToByteArray(x)
    local bytesY = floatToByteArray(y)
    local bytesZ = floatToByteArray(z)
    local grupoHexOrigem = "h " .. table.concat(bytesX, " ") .. " " .. table.concat(bytesY, " ") .. " " .. table.concat(bytesZ, " ")
    local bytesVX = floatToByteArray(posVeiculo.x)
    local bytesVY = floatToByteArray(posVeiculo.y)
    local bytesVZ = floatToByteArray(posVeiculo.z)
    local grupoHexVeiculo = "h " .. table.concat(bytesVX, " ") .. " " .. table.concat(bytesVY, " ") .. " " .. table.concat(bytesVZ, " ")
    gg.clearResults()
    gg.setRanges(gg.REGION_ANONYMOUS)
    gg.searchNumber(grupoHexOrigem, gg.TYPE_BYTE, false, gg.SIGN_EQUAL)
    local results = gg.getResults(9999)
    if #results == 0 then
      gg.alert("لم يتم العثور على نتائج للنقطة المحددة.")
      return Home()
    end
    local enderecosParaIgnorar = {
      GrupoPontoMapa[1].address,
      GrupoPontoMapa[2].address,
      GrupoPontoMapa[3].address
    }
    local resultadosFiltrados = {}
    do
      do
        for _FORV_23_, _FORV_24_ in ipairs(results) do
          local ignorar = false
          do
            do
              for _FORV_29_, _FORV_30_ in ipairs(enderecosParaIgnorar) do
                if _FORV_24_.address == _FORV_30_ then
                  ignorar = true
                  break
                end
              end
            end
          end
          if not ignorar then
            table.insert(resultadosFiltrados, _FORV_24_)
          end
        end
      end
    end
    if #resultadosFiltrados == 0 then
      gg.alert("تم العثور على النقطة الأصلية فقط. لا يوجد شيء للتعديل..")
    else
      gg.setValues(resultadosFiltrados)
      gg.editAll(grupoHexVeiculo, gg.TYPE_BYTE)
      gg.toast("『مجاني』 👑  Silk Road 👑")
    end
    gg.sleep(25000)
  until gg.isVisible()
  if gg.isVisible() then
    gg.setVisible(false)
if gg.alert("🇮🇶هل تريد التوقف عن المزرعة؟", "نعم", "لا") == 1 then
      Home()
    else
      FarmL()
    end
  end
end

function Roubo()
  menu_roubo_ativo = true
  local sapo = gg.multiChoice({
"🇮🇶اختر الموقع ",
"🇮🇶تحديد نقطة التفتيش ",
"🇮🇶سحب نقطة التفتيش ",
"🇮🇶⬅️العودة إلى القائمة "
  }, nil, "『مجاني』 👑  Silk Road 👑\n")
  if sapo == nil then
    return
  end
  if sapo[1] then
    escolherLoc()
  elseif sapo[2] then
    Ativaroo()
  elseif sapo[3] then
    GoPoint()
  elseif sapo[4] then
    menu_roubo_ativo = false
    Home()
    return
  end
end

function Ativaroo()
  gg.alert("‼️ ⚠️ انتبه! يجب أن تكون داخل مركبة 🚙\nانتظر ظهور خط أصفر حتى تصل إلى الوجهة المحددة قبل التفعيل‼️\n\nملاحظة.. تحتاج فقط لتحديد النقطة مرة واحدة")
  gg.clearResults()
  gg.setRanges(32)
  search("NavigationGraph", "0x50", true, false, 16)
  local resultsX = gg.getResults(1)
  if #resultsX == 0 then
    gg.alert("❗️يبدو أنك لم تحدد نقطة على الخريطة ❗️")
    return Home()
  end
  local COaddressesX = {}
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(resultsX) do
        table.insert(COaddressesX, {
          address = _FORV_6_.address
        })
      end
    end
  end
  GrupoPontoMapa = {}
  do
    do
      for _FORV_5_ = 1, #COaddressesX do
        local x = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address,
            flags = gg.TYPE_FLOAT
          }
        })
        local y = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address + 4,
            flags = gg.TYPE_FLOAT
          }
        })
        local z = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address + 8,
            flags = gg.TYPE_FLOAT
          }
        })
        if x[1].value ~= 0 and y[1].value ~= 0 and z[1].value ~= 0 then
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address,
            flags = gg.TYPE_FLOAT,
            value = x[1].value
          })
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address + 4,
            flags = gg.TYPE_FLOAT,
            value = y[1].value
          })
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address + 8,
            flags = gg.TYPE_FLOAT,
            value = z[1].value
          })
        end
      end
    end
  end
  gg.alert("✅")
  if #GrupoPontoMapa == 0 then
    gg.alert("❗️غير قادر على التقاط إحداثيات النقاط على الخريطة.")
    return Home()
  end
  if not posVeiculo or posVeiculo.x == 0 and posVeiculo.y == 0 and posVeiculo.z == 0 then
    gg.alert("❗️لم يتم التقاط موقع المركبة أو أنه غير صحيح. تأكد من وجودك داخل المركبة.")
    return Home()
  end
end

function GoPoint()
  local xAnterior, yAnterior, zAnterior
  local valoresAtualizados = gg.getValues({
    {
      address = GrupoPontoMapa[1].address,
      flags = gg.TYPE_FLOAT
    },
    {
      address = GrupoPontoMapa[2].address,
      flags = gg.TYPE_FLOAT
    },
    {
      address = GrupoPontoMapa[3].address,
      flags = gg.TYPE_FLOAT
    }
  })
  local x = valoresAtualizados[1].value
  local y = valoresAtualizados[2].value
  local z = valoresAtualizados[3].value
  xAnterior, yAnterior, zAnterior = x, y, z
  local bytesX = floatToByteArray(x)
  local bytesY = floatToByteArray(y)
  local bytesZ = floatToByteArray(z)
  local grupoHexOrigem = "h " .. table.concat(bytesX, " ") .. " " .. table.concat(bytesY, " ") .. " " .. table.concat(bytesZ, " ")
  local bytesVX = floatToByteArray(posVeiculo.x)
  local bytesVY = floatToByteArray(posVeiculo.y)
  local bytesVZ = floatToByteArray(posVeiculo.z)
  local grupoHexVeiculo = "h " .. table.concat(bytesVX, " ") .. " " .. table.concat(bytesVY, " ") .. " " .. table.concat(bytesVZ, " ")
  gg.clearResults()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.searchNumber(grupoHexOrigem, gg.TYPE_BYTE, false, gg.SIGN_EQUAL)
  local results = gg.getResults(9999)
  if #results == 0 then
    gg.alert("لم يتم العثور على نتائج للنقطة المحددة.")
    return Home()
  end
  local enderecosParaIgnorar = {
    GrupoPontoMapa[1].address,
    GrupoPontoMapa[2].address,
    GrupoPontoMapa[3].address
  }
  local resultadosFiltrados = {}
  do
    do
      for _FORV_21_, _FORV_22_ in ipairs(results) do
        local ignorar = false
        do
          do
            for _FORV_27_, _FORV_28_ in ipairs(enderecosParaIgnorar) do
              if _FORV_22_.address == _FORV_28_ then
                ignorar = true
                break
              end
            end
          end
        end
        if not ignorar then
          table.insert(resultadosFiltrados, _FORV_22_)
        end
      end
    end
  end
  if #resultadosFiltrados == 0 then
    gg.alert("Apenas o ponto original foi encontrado. Nada a editar.")
  else
    gg.setValues(resultadosFiltrados)
    gg.editAll(grupoHexVeiculo, gg.TYPE_BYTE)
    gg.toast("『مجاني』 👑  Silk Road 👑")
  end
end

function FarmAllSpeed()
  gg.alert("‼️❌ لا تستخدم هذه الوظيفة في وظائف أخرى‼️\nإذا استخدمتها قد تتعرض للحظر، تم إنشاؤها حصريًا لوظيفة البنك ‼️")
  local sapo = gg.multiChoice({
"🇮🇶اختر الموقع ",
"🇮🇶ابدأ المزرعة ",
"🇮🇶⬅️القائمة الرئيسية "
  }, nil, "『مجاني』 👑  Silk Road 👑\n")
  if sapo == nil then
    return
  end
  if sapo[1] then
    escolherLoc()
  end
  if sapo[2] then
    Ativaroa()
  end
  if sapo[3] then
    menu_roubo_ativo = false
    return gg.setVisible(true)
  end
end

function Ativaroa()
  gg.alert("‼️ ⚠️ انتبه! يجب أن تكون داخل مركبة 🚙\nانتظر ظهور الخط الأصفر حتى تصل إلى الوجهة المحددة قبل التفعيل‼️\n\nملاحظة: تحتاج فقط لتحديد النقطة مرة واحدة")
  gg.clearResults()
  gg.setRanges(32)
  search("NavigationGraph", "0x50", true, false, 16)
  local resultsX = gg.getResults(1)
  if #resultsX == 0 then
    gg.alert("❗️يبدو أنك لم تحدد نقطة على الخريطة ❗️")
    return Home()
  end
  local COaddressesX = {}
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(resultsX) do
        table.insert(COaddressesX, {
          address = _FORV_6_.address
        })
      end
    end
  end
  GrupoPontoMapa = {}
  do
    do
      for _FORV_5_ = 1, #COaddressesX do
        local x = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address,
            flags = gg.TYPE_FLOAT
          }
        })
        local y = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address + 4,
            flags = gg.TYPE_FLOAT
          }
        })
        local z = gg.getValues({
          {
            address = COaddressesX[_FORV_5_].address + 8,
            flags = gg.TYPE_FLOAT
          }
        })
        if x[1].value ~= 0 and y[1].value ~= 0 and z[1].value ~= 0 then
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address,
            flags = gg.TYPE_FLOAT,
            value = x[1].value
          })
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address + 4,
            flags = gg.TYPE_FLOAT,
            value = y[1].value
          })
          table.insert(GrupoPontoMapa, {
            address = COaddressesX[_FORV_5_].address + 8,
            flags = gg.TYPE_FLOAT,
            value = z[1].value
          })
        end
      end
    end
  end
  gg.alert("✅")
  if #GrupoPontoMapa == 0 then
    gg.alert("❗️غير قادر على التقاط إحداثيات النقاط على الخريطة.")
    return Home()
  end
  if not posVeiculo or posVeiculo.x == 0 and posVeiculo.y == 0 and posVeiculo.z == 0 then
    gg.alert("❗️لم يتم التقاط موقع المركبة أو أنه غير صحيح. تأكد من وجودك داخل المركبة..")
    return Home()
  end
  local xAnterior, yAnterior, zAnterior
  gg.setRanges(gg.REGION_C_DATA)
  gg.clearResults()
  gg.clearList()
  gg.searchNumber("-400107883", 4)
  local r = gg.getResults(gg.getResultsCount())
  gg.loadResults(r)
  do
    do
      for _FORV_9_, _FORV_10_ in ipairs(r) do
        _FORV_10_.address = _FORV_10_.address + 4
        _FORV_10_.flags = 4
      end
    end
  end
  gg.loadResults(r)
  gg.getResults(gg.getResultsCount())
  gg.editAll(1045313291, 4)
  Enabled_Function()
  repeat
    local valoresAtualizados = gg.getValues({
      {
        address = GrupoPontoMapa[1].address,
        flags = gg.TYPE_FLOAT
      },
      {
        address = GrupoPontoMapa[2].address,
        flags = gg.TYPE_FLOAT
      },
      {
        address = GrupoPontoMapa[3].address,
        flags = gg.TYPE_FLOAT
      }
    })
    local x = valoresAtualizados[1].value
    local y = valoresAtualizados[2].value
    local z = valoresAtualizados[3].value
    xAnterior, yAnterior, zAnterior = x, y, z
    local bytesX = floatToByteArray(x)
    local bytesY = floatToByteArray(y)
    local bytesZ = floatToByteArray(z)
    local grupoHexOrigem = "h " .. table.concat(bytesX, " ") .. " " .. table.concat(bytesY, " ") .. " " .. table.concat(bytesZ, " ")
    local bytesVX = floatToByteArray(posVeiculo.x)
    local bytesVY = floatToByteArray(posVeiculo.y)
    local bytesVZ = floatToByteArray(posVeiculo.z)
    local grupoHexVeiculo = "h " .. table.concat(bytesVX, " ") .. " " .. table.concat(bytesVY, " ") .. " " .. table.concat(bytesVZ, " ")
    gg.clearResults()
    gg.setRanges(gg.REGION_ANONYMOUS)
    gg.searchNumber(grupoHexOrigem, gg.TYPE_BYTE, false, gg.SIGN_EQUAL)
    local results = gg.getResults(9999)
    if #results == 0 then
      gg.alert("لم يتم العثور على نتائج للنقطة المحددة.")
      return Home()
    end
    local enderecosParaIgnorar = {
      GrupoPontoMapa[1].address,
      GrupoPontoMapa[2].address,
      GrupoPontoMapa[3].address
    }
    local resultadosFiltrados = {}
    do
      do
        for _FORV_24_, _FORV_25_ in ipairs(results) do
          local ignorar = false
          do
            do
              for _FORV_30_, _FORV_31_ in ipairs(enderecosParaIgnorar) do
                if _FORV_25_.address == _FORV_31_ then
                  ignorar = true
                  break
                end
              end
            end
          end
          if not ignorar then
            table.insert(resultadosFiltrados, _FORV_25_)
          end
        end
      end
    end
    if #resultadosFiltrados == 0 then
      gg.alert("تم العثور على النقطة الأصلية فقط. لا يوجد شيء للتعديل..")
    else
      gg.setValues(resultadosFiltrados)
      gg.editAll(grupoHexVeiculo, gg.TYPE_BYTE)
      gg.toast("『مجاني』 👑  Silk Road  👑")
    end
    gg.sleep(9000)
  until gg.isVisible()
  if gg.isVisible() then
    gg.setVisible(false)
if gg.alert("🇮🇶هل تريد التوقف عن المزرعة؟", "نعم", "لا") == 1 then
      gg.setRanges(gg.REGION_C_DATA)
      gg.clearResults()
      gg.clearList()
      gg.searchNumber("-400107883", 4)
      local r = gg.getResults(gg.getResultsCount())
      gg.loadResults(r)
      do
        do
          for _FORV_10_, _FORV_11_ in ipairs(r) do
            _FORV_11_.address = _FORV_11_.address + 4
            _FORV_11_.flags = 4
          end
        end
      end
      gg.loadResults(r)
      gg.getResults(gg.getResultsCount())
      gg.editAll(1041313291, 4)
      Enabled_Function()
      Home()
    else
      FarmL()
    end
  end
end

function escolherLoc()
  gg.alert("‼️ ⚠️ انتبه! يجب أن تكون خارج المركبة لاختيار الموقع 🧍‍♂️\n‼️")
  gg.setRanges(32)
  gg.clearResults()
  search("CharacterActor", "0x160", true, false, 16)
  gg.getResults(30)
  gg.editAll(100, 16)
  gg.sleep(80)
  local results = gg.getResults(30)
  local filtered = {}
  do
    do
      for _FORV_5_, _FORV_6_ in ipairs(results) do
        if _FORV_6_.value ~= 100 then
          table.insert(filtered, _FORV_6_)
        end
      end
    end
  end
  gg.loadResults(filtered)
  local t = gg.getResults(1)
  if #t == 0 then
    gg.alert("لم يتم العثور على بنية الأحرف.")
    return
  end
  local yAddr = t[1].address
  local xAddr = yAddr - 4
  local zAddr = yAddr + 4
  local valores = gg.getValues({
    {
      address = xAddr,
      flags = gg.TYPE_FLOAT
    },
    {
      address = yAddr,
      flags = gg.TYPE_FLOAT
    },
    {
      address = zAddr,
      flags = gg.TYPE_FLOAT
    }
  })
  posVeiculo = {
    x = valores[1].value,
    y = valores[2].value,
    z = valores[3].value
  }
  table.insert(addressesX, {address = xAddr})
  table.insert(addressesY, {address = yAddr})
  table.insert(addressesZ, {address = zAddr})
  gg.alert("✅️")
end

function floatToByteArray(float)
  local packed = string.pack("<f", float)
  local bytes = {}
  do
    do
      for _FORV_6_ = 1, #packed do
        table.insert(bytes, string.format("%02X", packed:byte(_FORV_6_)))
      end
    end
  end
  return bytes
end

endereco_xyz = {}
fly_ativo = false
direcao_atual = nil
ultimo_movimento = os.clock()
velocidade = 3
menu_roubo_ativo = false
fly_inicializado = false
z_posicao_minima = nil
z_posicao_inicial = nil
function MenuControle()
  local m = gg.choice({
"🔓 فتح القفل ",
    "⬆️ صعود ",
    "⬇️ نزول ",
    "⛔ إيقاف الحركة ",
    "➡️ إلى اليمين ",
    "⬅️ إلى اليسار ",
    "⬆️ إلى الأمام ",
    "⬇️ إلى الخلف ",
    "↩️ القائمة الرئيسية "
  }, nil, "🚗 قائمة الطيران بالسيارة")
  if m == nil then
    return
  end
  function DesbloquearFlyCar()
    local SearchTpCar = "h AE C5 9D 74 0A D7 23 3C CD CC 4C 3D"
    gg.setRanges(32)
    gg.clearResults()
    gg.searchNumber(SearchTpCar, 1)
    gg.refineNumber("-82", 1)
    local t = gg.getResults(20)
    do
      do
        for _FORV_5_, _FORV_6_ in ipairs(t) do
          _FORV_6_.address = _FORV_6_.address + 96
          _FORV_6_.flags = gg.TYPE_FLOAT
        end
      end
    end
    gg.loadResults(t)
    local r = gg.getResults(#t)
    endereco_xyz = {}
    do
      do
        for _FORV_6_, _FORV_7_ in ipairs(r) do
          local addrZ = _FORV_7_.address
          table.insert(endereco_xyz, {
            x = addrZ + 4,
            y = addrZ - 4,
            z = addrZ
          })
        end
      end
    end
    if #endereco_xyz > 0 then
      gg.toast("تم فتح العناوين بنجاح!")
    else
      gg.alert("لم يتم العثور على عنوان.")
    end
  end
  
  if m == 1 then
    DesbloquearFlyCar()
  else
    if m == 2 then
      if z_posicao_inicial == nil then
        local leituraZ = {
          address = endereco_xyz[1].z,
          flags = gg.TYPE_FLOAT
        }
        local z_atual = gg.getValues({leituraZ})[1].value + 2
        z_posicao_inicial = z_atual + 2
        z_posicao_minima = z_atual + 2
        gg.toast("تم حفظ موضع Z بنجاح!")
      end
      direcao_atual = "subir"
      fly_ativo = true
      gg.setVisible(false)
      do return end
      return
    end
    if m == 3 then
      if z_posicao_minima == nil then
        gg.toast("يجب عليك الصعود قبل النزول.")
        return
      end
      direcao_atual = "descer"
      fly_ativo = true
      gg.setVisible(false)
      do return end
      return
    end
    if m == 4 then
      fly_ativo = false
      direcao_atual = nil
      gg.toast("توقفت الحركة.")
      do return end
      return
    end
    if m == 5 then
      if #endereco_xyz == 0 then
        gg.alert("يجب عليك أولاً فتح قفل السيارة الطائرة قبل التحرك إلى اليمين.")
        return
      end
      direcao_atual = "direita"
      fly_ativo = true
      gg.setVisible(false)
      do return end
      return
    end
    if m == 6 then
      if #endereco_xyz == 0 then
        gg.alert("يجب عليك أولاً فتح قفل السيارة الطائرة قبل التحرك إلى اليسار.")
        return
      end
      direcao_atual = "esquerda"
      fly_ativo = true
      gg.setVisible(false)
      do return end
      return
    end
    if m == 7 then
      if #endereco_xyz == 0 then
        gg.alert("يجب عليك أولاً فتح السيارة الطائرة قبل المضي قدمًا..")
        return
      end
      direcao_atual = "frente"
      fly_ativo = true
      gg.setVisible(false)
      do return end
      return
    end
    if m == 8 then
      if #endereco_xyz == 0 then
        gg.alert("يجب عليك أولاً فتح قفل السيارة الطائرة قبل التحرك للخلف..")
        return
      end
      direcao_atual = "tras"
      fly_ativo = true
      gg.setVisible(false)
      do return end
      return
    end
    if m == 9 then
      menu_roubo_ativo = false
      return gg.setVisible(true)
    end
  end
end

function InicializarFly()
  if fly_inicializado or #endereco_xyz == 0 then
    if #endereco_xyz == 0 then
      gg.alert("يجب عليك أولاً استخدام فتح السيارة الطائرة في القائمة.")
    end
    return
  end
  gg.toast("الإحداثيات المحملة!")
  fly_inicializado = true
end

function MoverContinuamente()
  local leitura = {}
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(endereco_xyz) do
        table.insert(leitura, {
          address = _FORV_5_.x,
          flags = gg.TYPE_FLOAT
        })
        table.insert(leitura, {
          address = _FORV_5_.y,
          flags = gg.TYPE_FLOAT
        })
        table.insert(leitura, {
          address = _FORV_5_.z,
          flags = gg.TYPE_FLOAT
        })
      end
    end
  end
  local valores = gg.getValues(leitura)
  local edits = {}
  local index = 1
  do
    do
      for _FORV_7_, _FORV_8_ in ipairs(endereco_xyz) do
        local valX = valores[index].value
        local valY = valores[index + 1].value
        local valZ = valores[index + 2].value
        index = index + 3
        if direcao_atual == "frente" then
          table.insert(edits, {
            address = _FORV_8_.y,
            flags = gg.TYPE_FLOAT,
            value = valY + velocidade
          })
        elseif direcao_atual == "tras" then
          table.insert(edits, {
            address = _FORV_8_.y,
            flags = gg.TYPE_FLOAT,
            value = valY - velocidade
          })
        elseif direcao_atual == "direita" then
          table.insert(edits, {
            address = _FORV_8_.x,
            flags = gg.TYPE_FLOAT,
            value = valX + velocidade
          })
        elseif direcao_atual == "esquerda" then
          table.insert(edits, {
            address = _FORV_8_.x,
            flags = gg.TYPE_FLOAT,
            value = valX - velocidade
          })
        elseif direcao_atual == "subir" then
          table.insert(edits, {
            address = _FORV_8_.z,
            flags = gg.TYPE_FLOAT,
            value = valZ + velocidade,
            freeze = true
          })
        elseif direcao_atual == "descer" then
          local novoZ = valZ - velocidade
          if novoZ < z_posicao_minima then
            novoZ = z_posicao_minima
          end
          table.insert(edits, {
            address = _FORV_8_.z,
            flags = gg.TYPE_FLOAT,
            value = novoZ,
            freeze = true
          })
        end
      end
    end
  end
  gg.setValues(edits)
  if direcao_atual == "subir" or direcao_atual == "descer" then
    gg.addListItems(edits)
  end
end

local libBase, il2cpp
local ranges = gg.getRangesList("libil2cpp.so")
do
  do
    for _FORV_26_, _FORV_27_ in ipairs(ranges) do
      if _FORV_27_.state == "Xa" then
        il2cpp = _FORV_27_.start
        break
      end
    end
  end
end
function CreateHook(Address1, Address2)
  gg.setRanges(16428)
  gg.clearResults()
  gg.clearList()
  local tt = {}
  tt[1] = {}
  tt[1].address = il2cpp + Address2
  tt[1].flags = 32
  gg.addListItems(tt)
  gg.loadResults(gg.getListItems())
  EditValue = gg.getResults(1)[1].address
  gg.clearResults()
  gg.clearList()
  local tt = {}
  tt[1] = {}
  tt[1].address = il2cpp + Address1
  tt[1].flags = 32
  gg.addListItems(tt)
  gg.loadResults(gg.getListItems())
  gg.getResults(50)
  gg.clearList()
  gg.searchPointer(0)
  OriginalValue = gg.getResults(1)[1].value
  gg.getResults(50)
  gg.sleep(500)
  gg.editAll(EditValue, 32)
  gg.sleep(300)
end

function EndHook()
  gg.clearResults()
  gg.clearList()
  gg.searchNumber(EditValue, 32)
  gg.getResults(50)
  gg.editAll(OriginalValue, 32)
end

function Mineiro()
  manuel = gg.multiChoice({
"🇮🇶مزرعة تلقائية بدون رسوم متحركة",
"🇮🇶مزرعة أوتوماتيكية"
  }, nil, "『مجاني』 👑 Silk Road  👑\n")
  if manuel == nil then
    return
  end
  if manuel[1] then
    anim()
  end
  if manuel[2] then
    auto()
  end
end

function anim()
  minerSleep()
end

function minerSleep()
  gg.toast("تنشيط نوم مينر...")
  gg.clearResults()
  gg.setRanges(gg.REGION_ANONYMOUS)
  gg.searchNumber("1001;1002;1003;1004", gg.TYPE_QWORD, false, gg.SIGN_EQUAL, 0, -1)
  gg.refineNumber("1001;1002;1003;1004", gg.TYPE_QWORD)
  local results = gg.getResults(gg.getResultsCount())
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(results) do
        _FORV_5_.value = 1004
        _FORV_5_.freeze = false
      end
    end
  end
  gg.setValues(results)
  gg.toast("تمت إزالة الرسوم المتحركة")
end

function anim()
  minerSleep()
end

function auto()
  minerSleep()
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 1A FF 1A 45 B9 34 46 42 33 14 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 78 34 BC 44 37 7C BE 41 E6 05 18 44", 1)
  gg.toast("10%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h B2 0E 1B 45 96 88 46 42 01 02 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 2B 60 1B 45 E8 C0 47 42 A4 FE 1B 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 34 79 1B 45 96 62 48 42 A4 5C 1B 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h B9 8F 1B 45 BF DA 3D 42 ED 27 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("20%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 0C B5 1B 45 D9 73 48 42 68 95 1B 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 6F CC 1B 45 61 9C 48 42 26 4F 1B 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 26 D3 1B 45 D2 DA 3D 42 03 06 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 6D EC 1B 45 CF DA 3D 42 3C 57 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("30%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 4F 04 1C 45 F0 80 34 42 F6 F6 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 95 23 1C 45 F0 80 34 42 88 65 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h CF 49 1C 45 19 46 66 42 BF 71 21 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h B8 58 1C 45 2B 47 64 42 91 9E 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("40%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 8B 5C 1C 45 DF B4 49 42 8D 52 1B 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 4E A1 1C 45 EF 80 34 42 94 DE 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h BA AF 1C 45 F0 80 34 42 FD 43 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h E7 CB 1C 45 F0 80 34 42 21 BE 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("50%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 45 E5 1C 45 FC DA 3D 42 E6 79 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 11 00 1D 45 E4 DA 3D 42 F9 D9 18 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 53 20 1D 45 F0 80 34 42 93 BD 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 8C 32 1D 45 F0 80 34 42 18 00 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("60%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 4F 44 1D 45 F0 80 34 42 F6 F6 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 11 5D 1D 45 F0 80 34 42 DC 91 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 95 63 1D 45 F0 80 34 42 88 65 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h E9 96 1D 45 EB 54 47 42 FF 6A 1E 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("70%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 1F 97 1D 45 F0 80 34 42 03 EF 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 5C A4 1D 45 F0 80 34 42 9E B4 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 7A A6 1D 45 F0 80 34 42 C8 7F 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 2B B0 1D 45 1A 67 47 42 40 91 1E 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h D0 DB 1D 45 F0 80 34 42 9D 08 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 7F EA 1D 45 A5 67 47 42 B9 53 1E 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("80%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 13 3D 1E 45 4A 73 34 42 AC 82 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h A0 40 1E 45 4A 73 34 42 5E B8 1C 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 2B F1 1E 45 3D A3 62 42 FD 0B 21 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h FE 28 1F 45 A6 44 65 42 CD 56 21 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h A2 4B 1F 45 86 12 64 42 94 15 21 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h B8 78 1F 45 2B 47 64 42 91 9E 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h AF 86 1F 45 68 92 64 42 08 FE 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 14 C7 1F 45 55 C5 66 42 7D 3A 21 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h DC E1 1F 45 59 99 66 42 AD A4 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 0E 11 20 45 06 61 67 42 67 DC 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 1C 3E 20 45 3D 9B 67 42 D1 B8 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 8F 53 20 45 9C 90 52 42 BC 1B 1E 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("90%")
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 23 86 20 45 2F EC 3D 42 42 4D 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h B6 8A 20 45 81 45 69 42 5D 37 20 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h A2 92 20 45 87 91 52 42 DC 2D 1E 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 8D 93 20 45 C0 A4 54 42 B2 DF 1D 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h E4 C7 20 45 E5 DA 3D 42 BA 11 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 45 E5 20 45 FC DA 3D 42 E6 79 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 50 0F 21 45 D1 DA 3D 42 06 4F 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h E7 57 21 45 BF DA 3D 42 5B 11 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 01 5F 21 45 EA DA 3D 42 C2 68 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 11 60 21 45 E4 DA 3D 42 F9 D9 18 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h DC A7 21 45 BF DA 3D 42 DC 0A 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h C1 B8 21 45 BF DA 3D 42 1E 4F 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h B9 CF 21 45 BF DA 3D 42 ED 27 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 9A F6 21 45 BD DA 3D 42 0F 52 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 26 13 22 45 D2 DA 3D 42 03 06 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.clearList()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("h 6D 2C 22 45 CF DA 3D 42 3C 57 19 45", 1)
  gg.getResults(9999)
  gg.editAll("h 85 C5 23 45 47 91 3D 42 7D F6 1C 45", 1)
  gg.toast("100%")
  gg.toast("تم تفعيل المزرعة التلقائية ✅️")
end

local gg = gg
local clock = os.clock
local toast = gg.toast
local info = gg.getTargetInfo()
local LibTable = {}
function isProcess64Bit()
  local regions = gg.getRangesList()
  local lastAddress = regions[#regions]["end"]
  return lastAddress >> 32 ~= 0
end

local ISA = isProcess64Bit()
function ISAOffsets()
  if ISA == false then
    edi = "+0x"
    ed = "-0x"
  elseif ISA == true then
    edi = "0x"
    ed = "-0x"
  end
end

ISAOffsets()
function ISAOffsetss()
  if ISA == false then
    edit = "~A B " .. edits
  elseif ISA == true then
    edit = "~A8 B\t [PC,#" .. edits .. "]"
  end
end

xg = {}
function gets(g)
  gg.loadResults(end_hook)
  xg[g] = gg.getResults(gg.getResultsCount())
  gg.clearResults()
end

function libs(loz)
  liby = 1
  libf = 0
  libzz = loz
  libx = gg.getRangesList(loz)
  do
    do
      for _FORV_4_, _FORV_5_ in ipairs(libx) do
        if libx[_FORV_4_].state == "Xa" then
          libz = loz .. "[" .. liby .. "].start"
          xand = gg.getRangesList(loz)[liby].start
          libf = 1
          break
        end
        liby = liby + 1
      end
    end
  end
  lib = xand
end

function __()
  xHEX = string.format("%X", aaaa)
  if #xHEX > 8 then
    act = #xHEX - 8 + 1
    xHEX = string.sub(xHEX, act)
  end
  edits = edi .. xHEX
  ISAOffsetss()
end

function _()
  aaa = b - a
  xHEX = string.format("%X", aaa)
  if #xHEX > 8 then
    act = #xHEX - 8 + 1
    xHEX = string.sub(xHEX, act)
  end
  edits = ed .. xHEX
  ISAOffsetss()
end

function endhook(cc, g)
  LibStart = lib
  local eh = {}
  eh[1] = {
    address = LibStart + cc,
    flags = gg.TYPE_DWORD,
    value = xg[g][1].value,
    freeze = true
  }
  gg.addListItems(eh)
  gg.clearList()
end

function hook_void(cc, bb, g)
  LibStart = lib
  local m = {}
  m[1] = {
    address = LibStart + bb,
    flags = gg.TYPE_DWORD
  }
  gg.addListItems(m)
  a = m[1].address
  gg.clearList()
  local p = {}
  p[1] = {
    address = LibStart + cc,
    flags = gg.TYPE_DWORD
  }
  gg.addListItems(p)
  gg.loadResults(p)
  end_hook = gg.getResults(1)
  gets(g)
  local n = {}
  n[1] = {
    address = LibStart + cc,
    flags = gg.TYPE_DWORD
  }
  gg.addListItems(n)
  b = n[1].address
  gg.clearResults()
  gg.clearList()
  aaaa = a - b
  if tonumber(aaaa) < 0 then
    _()
  end
  if tonumber(aaaa) > 0 then
    __()
  end
  local n = {}
  n[1] = {
    address = LibStart + cc,
    flags = gg.TYPE_DWORD,
    value = edit,
    freeze = true
  }
  gg.addListItems(n)
  gg.clearList()
end

libs("libil2cpp.so")
 
function field()
    print("مرحبا")
    -- بعض الأكواد
end


function Exit()
    safeAlert("👋 الوداع")
    os.exit()
end

-- =============================
-- تشغيل دائم
-- =============================

gg.setVisible(false)
gg.toast('🔥 اضغط أيقونة 『مجاني』 👑  Silk Road  👑 للبدء 👆🔥')

while true do
    if gg.isVisible(true) then
        gg.setVisible(false)
        Home()
    end
    gg.sleep(100)
end
