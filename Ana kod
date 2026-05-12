import streamlit as st
import numpy as np
import matplotlib.pyplot as plt
from qiskit import QuantumCircuit
from qiskit.quantum_info import Statevector
from qiskit.visualization import plot_bloch_multivector, plot_state_city

st.set_page_config(page_title="Bell State Observer", layout="wide")

# Matrix - Siber Güvenlik Teması (CSS)
st.markdown("""
    <style>
    .main { background-color: #000000; }
    div[data-testid="stMarkdownContainer"] { color: #00FF41; font-family: 'Courier New', monospace; }
    .stSelectbox label { color: #00FF41 !important; }
    .stMetric { background-color: #0a0a0a; border: 1px solid #00FF41; padding: 10px; border-radius: 5px; }
    </style>
    """, unsafe_allow_html=True)

st.markdown("<h1 style='text-align: center; color: #00FF41; text-shadow: 0 0 15px #00FF41;'> KUANTUM DOLANIKLIK (BELL DURUMLARI)</h1>", unsafe_allow_html=True)

st.markdown("""
<div style='border: 1px solid #00FF41; padding: 15px; border-radius: 5px; background-color: #050505;'>
    [BİLGİ]: İki farklı kubitin kaderinin birbirine bağlandığı 'Dolaşıklık' (Entanglement) gözlemleniyor. 
    Bir kubit üzerindeki ölçüm, ışık hızından bağımsız olarak diğerinin durumunu anında belirler.
</div>
""", unsafe_allow_html=True)

# İnteraktif Seçim Alanı
st.sidebar.markdown("### [CONTROL_PANEL]")
bell_choice = st.sidebar.selectbox(
    "Oluşturulacak Bell Durumunu Seçin:",
    ["|Φ+⟩", "|Φ-⟩", "|Ψ+⟩", "|Ψ-⟩"]
)

# Kuantum Devresi Oluşturma
qc = QuantumCircuit(2)

if bell_choice == "|Φ+⟩":
    qc.h(0)
    qc.cx(0, 1)
    desc = "Her iki kubit aynı anda ya 0 ya da 1'dir. (Maksimum Korelasyon)"
elif bell_choice == "|Φ-⟩":
    qc.x(0)
    qc.h(0)
    qc.cx(0, 1)
    desc = "Kubitler aynıdır ancak aralarında faz farkı (180°) vardır."
elif bell_choice == "|Ψ+⟩":
    qc.x(1)
    qc.h(0)
    qc.cx(0, 1)
    desc = "Kubitler her zaman birbirinin zıttıdır (Biri 0 ise diğeri 1)."
elif bell_choice == "|Ψ-⟩":
    qc.x(0)
    qc.x(1)
    qc.h(0)
    qc.cx(0, 1)
    qc.z(0)
    qc.z(1)
    desc = "Antisimetrik durum. Kubitler zıttır ve faz farkı bulunur."

state = Statevector.from_instruction(qc)

# Görselleştirme Alanı
col1, col2 = st.columns(2)

with col1:
    st.markdown("### Bloch Küreleri (Ayrı Bakış)")
    # İki kubitin durumunu yan yana gösterir
    fig1 = plot_bloch_multivector(state)
    fig1.patch.set_facecolor('black')
    st.pyplot(fig1)
    st.caption("Not: Dolaşık sistemlerde bireysel kubitler 'belirsiz' (kürenin merkezinde) görünür.")

with col2:
    st.markdown("### Sistem Matrisi")
    # Sistemin yoğunluk matrisini 3D sütunlarla gösterir
    fig2 = plot_state_city(state, color=['#00FF41', '#008F11'])
    fig2.patch.set_facecolor('black')
    st.pyplot(fig2)

# Bilimsel Analiz Raporu
st.markdown(f"""
<div style="background-color: #0a0a0a; padding: 20px; border-left: 5px solid #00FF41; margin-top: 20px;">
    <h4 style="color: #00FF41; margin-top: 0;">🔍 ANALİZ RAPORU: {bell_choice}</h4>
    <p><b>DURUM TANIMI:</b> {desc}</p>
    <p><b>MATEMATİKSEL FORM:</b> Bu durum, iki kubitin klasik bir şekilde açıklanamayacak 
    istatistiksel bir bağ kurduğunu kanıtlar. Bu bağ, kuantum teleportasyon ve kriptografinin temelidir.</p>
    <hr style="border: 0.1px solid #333;">
    <p style="font-size: 12px; color: #888;">[LOG]: Devreye Hadamard (H) ve CNOT kapıları uygulandı. Dolaşıklık doğrulandı.</p>
</div>
""", unsafe_allow_html=True)

st.sidebar.write("---")
st.sidebar.markdown("**[DEVRE ŞEMASI]**")
st.sidebar.code(qc.draw(output='text'))
