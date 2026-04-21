import streamlit as st
import pdfplumber
import pandas as pd

st.set_page_config(page_title="Трейдинг Календар", layout="wide")
st.title("📈 Мій Трейдинг Аналітик")

uploaded_file = st.file_uploader("Завантажте PDF-звіт від брокера", type="pdf")

if uploaded_file:
    with pdfplumber.open(uploaded_file) as pdf:
        text = "\n".join([page.extract_text() for page in pdf.pages if page.extract_text()])
    
    st.success("Файл успішно завантажено та прочитано!")
    
    # Демонстраційна таблиця (налаштуємо під ваші реальні звіти пізніше)
    st.subheader("Ваші результати за місяць")
    df = pd.DataFrame({
        "Дата": ["04.04.2026", "12.04.2026"],
        "Інструмент": ["AAPL", "BTC/USD"],
        "Прибуток/Збиток ($)": [250.00, 180.00],
        "Комісія ($)": [2.50, 4.00],
        "Чистий результат ($)": [247.50, 176.00]
    })
    
    st.dataframe(df, use_container_width=True)
    
    total_profit = df["Чистий результат ($)"].sum()
    st.metric(label="Загальний чистий заробіток", value=f"${total_profit}")
    
    st.info("Додаток працює! Наступним кроком буде налаштування алгоритму для витягування цифр саме з ваших PDF-звітів.")
# -
Розрахунок заробітку
