import random
ANIME=["ايرين", "ناروتو", "لوفي", "غوكو", "ساسكي", "ميكاسا", "ليفاي", "زورو", "سانجي", "كاكاشي", "ايتاشي", "مادارا", "هيناتا", "ساكورا", "جيرايا", "تسونادي", "اوروتشيمارو", "كيلوا", "غون", "كورابيكا", "هيسوكا", "نيترو", "ميريوم", "سايتاما", "جينوس", "موب", "تاتسوماكي", "دينجي", "باور", "اكي", "ماكيما", "تانجيرو", "نيزوكو", "زينيتسو", "اينوسكي", "رينغوكو", "غيومي", "موزان", "غيو", "شينوبو", "استا", "يونو", "نويل", "يوليوس", "بلاك كلوفر", "دeku", "باكوغو", "تودوروكي", "اول مايت", "شوتو", "ايري", "شigaraki", "يوجي", "ميغومي", "نوبارا", "غوجو", "سوكونا", "نانامي", "ماكي", "توجي", "سبايك", "فاش", "ادوارد", "الفونس", "روي", "سايمون", "كامينا", "يоко", "غورين", "لايت", "ال", "نير", "ميسا", "سبايك شيغل", "ايتشيغو", "روكيا", "بياكويا", "كينباتشي", "اوريهيمي", "توشيرو", "ايزن", "يوريتشي", "ناتسو", "غري", "ايرزا", "لوسی", "غاجيل", "ويندي", "جيرار", "سبارو", "اش", "ل", "كيرا", "كونان", "ران", "هيجي", "كايتو كيد", "سينكو", "كروم", "كوهاكو"]
COUNTRIES={"🇪🇬": "مصر", "🇸🇦": "السعودية", "🇦🇪": "الإمارات", "🇶🇦": "قطر", "🇰🇼": "الكويت", "🇧🇭": "البحرين", "�🇴🇲": "عمان", "🇾🇪": "اليمن", "🇮🇶": "العراق", "🇸🇾": "سوريا", "🇱🇧": "لبنان", "🇯🇴": "الأردن", "🇵🇸": "فلسطين", "🇱🇾": "ليبيا", "🇹🇳": "تونس", "🇩🇿": "الجزائر", "🇲🇦": "المغرب", "🇲🇷": "موريتانيا", "🇸🇩": "السودان", "🇸🇴": "الصومال", "🇩🇯": "جيبوتي", "🇰🇲": "جزر القمر", "🇯🇵": "اليابان", "🇨🇳": "الصين", "🇰🇷": "كوريا الجنوبية", "🇰🇵": "كوريا الشمالية", "🇮🇳": "الهند", "🇵🇰": "باكستان", "🇧🇩": "بنغلاديش", "🇮🇩": "إندونيسيا", "🇲🇾": "ماليزيا", "🇹🇭": "تايلاند", "🇻🇳": "فيتنام", "🇵🇭": "الفلبين", "🇸🇬": "سنغافورة", "🇹🇷": "تركيا", "🇮🇷": "إيران", "🇦🇫": "أفغانستان", "🇫🇷": "فرنسا", "🇩🇪": "ألمانيا", "🇮🇹": "إيطاليا", "🇪🇸": "إسبانيا", "🇵🇹": "البرتغال", "🇬🇧": "بريطانيا", "🇮🇪": "أيرلندا", "🇳🇱": "هولندا", "🇧🇪": "بلجيكا", "🇨🇭": "سويسرا", "🇦🇹": "النمسا", "🇸🇪": "السويد", "🇳🇴": "النرويج", "🇩🇰": "الدنمارك", "🇫🇮": "فنلندا", "🇵🇱": "بولندا", "🇬🇷": "اليونان", "🇷🇺": "روسيا", "🇺🇦": "أوكرانيا", "🇺🇸": "أمريكا", "🇨🇦": "كندا", "🇲🇽": "المكسيك", "🇧🇷": "البرازيل", "🇦🇷": "الأرجنتين", "🇨🇱": "تشيلي", "🇨🇴": "كولومبيا", "🇵🇪": "بيرو", "🇻🇪": "فنزويلا", "🇳🇬": "نيجيريا", "🇪🇹": "إثيوبيا", "🇰🇪": "كينيا", "🇿🇦": "جنوب أفريقيا", "🇬🇭": "غانا", "🇸🇳": "السنغال", "🇦🇺": "أستراليا", "🇳🇿": "نيوزيلندا"}
active_games={}

def can_play(db,sender):
    from database import get_user
    s=db["settings"]
    u=get_user(db,sender)
    if u["banned_game"]: return False
    if s["games_locked"] and not u["is_admin"]: return False
    return True

def handle_games(db,sender,text):
    t=text.strip()
    if not can_play(db,sender): return "⛔ أنت محظور من الألعاب أو الألعاب مقفولة"
    if t=="تفكيك":
        name=random.choice(ANIME); active_games[sender]=("تفكيك",name)
        return f"🧩 فكك الاسم: {name}\nاكتب الحروف مفككة: {' '.join(list(name))} مثال؟ لا! اكتب انت بسرعة"
    if t=="تركيب":
        name=random.choice(ANIME); active_games[sender]=("تركيب",name)
        return f"🧩 ركب الاسم: {' '.join(list(name))}"
    if t=="كتابة":
        s="السرعة سر النجاح"; active_games[sender]=("كتابة",s)
        return f"⌨️ اكتب الجملة بنفس الشكل بسرعة:\n{s}"
    if t=="اعلام":
        flag, country = random.choice(list(COUNTRIES.items())); active_games[sender]=("اعلام",country)
        return f"{flag} ما اسم هذه الدولة؟"
    # تحقق من الإجابة
    if sender in active_games:
        typ, answer = active_games[sender]
        # تبسيط: قارن بعد إزالة المسافات
        if text.replace(" ","").strip()==answer.replace(" ",""):
            del active_games[sender]
            from database import get_user
            u=get_user(db,sender); u["wins"]+=1; u["xp"]+=20; u["balance"]+=10
            return f"🎉 صح! فزت +10 MToken و +20 XP"
    return None

import random as _rand
def handle_new_games(db,sender,text):
    from database import get_user
    t=text.strip(); u=get_user(db,sender)
    if t=="اسرع":
        e=_rand.choice(["😂","🔥","🍕","🚀","🐱"])
        active_games[sender]=("اسرع",e)
        return f"⚡ أسرع واحد يبعت هذا الايموجي: {e}"
    if t=="رياضيات":
        a=_rand.randint(1,50); b=_rand.randint(1,50)
        ans=str(a+b); active_games[sender]=("رياضيات",ans)
        return f"🔢 حل بسرعة: {a} + {b} = ؟"
    if t=="خمن":
        n=_rand.randint(1,20); active_games[sender]=("خمن",str(n))
        return "🎯 خمنت رقم من 1 لـ 20، اكتب تخمينك"
    if t.startswith("حجرة") or "ورقة" in t or "مقص" in t:
        choices=["حجرة","ورقة","مقص"]
        bot=_rand.choice(choices)
        # استخراج اختيار اللاعب
        player=None
        for c in choices:
            if c in t: player=c; break
        if not player: return "اكتب: حجرة أو ورقة أو مقص"
        if player==bot: return f"🤝 تعادل! البوت اختار {bot}"
        win=(player=="حجرة" and bot=="مقص") or (player=="ورقة" and bot=="حجرة") or (player=="مقص" and bot=="ورقة")
        if win:
            u["wins"]+=1; u["xp"]+=15; u["balance"]+=15
            return f"🎉 فزت! البوت اختار {bot} +15 MToken"
        else:
            return f"😢 خسرت! البوت اختار {bot}"
    # تحقق إجابات الألعاب الجديدة
    if sender in active_games:
        typ,answer=active_games[sender]
        if typ in ("اسرع","رياضيات","خمن") and text.strip()==answer:
            del active_games[sender]
            u["wins"]+=1; u["xp"]+=15; u["balance"]+=15
            return f"🎉 صح! +15 MToken و +15 XP"
    return None
_orig_handle_games=handle_games
def handle_games(db,sender,text):
    r=_orig_handle_games(db,sender,text)
    if r: return r
    return handle_new_games(db,sender,text)
