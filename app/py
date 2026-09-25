import streamlit as st

# База слов и рангов
words_easy = {"family": "семья", "hand": "рука", "people": "люди", "evening": "вечер", "minute": "минута"}
words_medium = {"believe": "верить", "feel": "чувствовать", "make": "делать", "open": "открывать", "think": "думать"}
words_hard = {"rural": "деревенский", "fortune": "удача", "exercise": "упражнение", "suggest": "предлагать", "except": "кроме"}
levels = {0: "Нулевой", 1: "Так себе", 2: "Можно лучше", 3: "Норм", 4: "Хорошо", 5: "Отлично"}

st.set_page_config(page_title="Викторина-Переводчик", page_icon="📝")
st.title("📝 Викторина по английскому языку")

# Инициализация состояний игры
if "game_started" not in st.session_state:
    st.session_state.game_started = False
if "answers" not in st.session_state:
    st.session_state.answers = {}

# Выбор сложности
if not st.session_state.game_started:
    st.subheader("Выберите уровень сложности, чтобы начать:")
    choice = st.radio("Сложность:", ["Легкий", "Средний", "Сложный"], horizontal=True)
    
    if st.button("Начать игру 🚀", use_container_width=True):
        if choice == "Легкий":
            st.session_state.current_words = words_easy
        elif choice == "Средний":
            st.session_state.current_words = words_medium
        else:
            st.session_state.current_words = words_hard
            
        st.session_state.game_started = True
        st.session_state.answers = {}
        st.rerun()

# Игровой процесс
else:
    st.subheader("Переведите следующие слова:")
    
    # Форма для ввода ответов
    with st.form("quiz_form"):
        user_inputs = {}
        for word_eng, word_rus in st.session_state.current_words.items():
            word_len = len(word_rus)
            first_letter = word_rus[0]
            
            label = f"Слово: **{word_eng}** ({word_len} букв, начинается на '{first_letter}')"
            user_inputs[word_eng] = st.text_input(label, key=word_eng).strip().lower()
            
        submit = st.form_submit_button("Узнать результаты 📊")
        
    if submit:
        correct_words = []
        incorrect_words = []
        
        for word_eng, word_rus in st.session_state.current_words.items():
            if user_inputs[word_eng] == word_rus.lower():
                st.session_state.answers[word_eng] = True
                correct_words.append(word_eng)
            else:
                st.session_state.answers[word_eng] = False
                incorrect_words.append(word_eng)
                
        correct_count = sum(st.session_state.answers.values())
        rank = levels.get(correct_count, "Без ранга")
        
        st.success(f"### Ваш ранг: {rank} ({correct_count} из 5)")
        
        col1, col2 = st.columns(2)
        with col1:
            st.write("**✅ Правильно:**")
            if correct_words:
                for w in correct_words:
                    st.write(f"- {w} ({st.session_state.current_words[w]})")
            else:
                st.write("Ни одного слова 😢")
                
        with col2:
            st.write("**❌ Неправильно:**")
            if incorrect_words:
                for w in incorrect_words:
                    st.write(f"- {w} (правильно: {st.session_state.current_words[w]})")
            else:
                st.write("Ошибок нет! 🎉")
                
        if st.button("Играть снова 🔄"):
            st.session_state.game_started = False
            st.rerun()
