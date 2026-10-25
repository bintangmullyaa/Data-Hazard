# Simulasi Data Hazard & Instruction-Level Parallelism (ILP)

Repositori ini berisi simulasi dan analisis mengenai **Instruction-Level Parallelism (ILP)** serta penanganan **Data Hazard** pada mata kuliah Organisasi dan Arsitektur Komputer.

---

## 📖 Deskripsi Proyek

Proyek ini bertujuan untuk:
1. **Mensimulasikan Eksekusi Instruksi**: Membandingkan siklus eksekusi antara model sekuensial (satu per satu) dengan model paralel (ILP) untuk melihat peningkatan performa (*speedup* dan efisiensi).
2. **Mendeteksi Data Hazard**:
   * **RAW (*Read After Write*)**: Ketergantungan data sejati (*True Data Dependency*).
   * **WAR (*Write After Read*)**: Ketergantungan nama/semu (*Anti-Dependency*).
   * **WAW (*Write After Write*)**: Ketergantungan output (*Output Dependency*).
3. **Mitigasi Hazard WAR dengan Register Renaming**: Mendemonstrasikan bagaimana prosesor modern mengatasi ketergantungan semu (WAR) dengan mengganti nama register tujuan secara dinamis, sehingga instruksi yang sebelumnya terhambat dapat dieksekusi secara paralel.
4. **Visualisasi Graf Dependensi**: Memvisualisasikan alur dependensi instruksi dalam bentuk diagram graf terarah (*Directed Graph*), serta membandingkan grafik sebelum dan sesudah diterapkannya *Register Renaming*.

---

## 📦 Requirements & Instalasi

Proyek ini menggunakan **Python 3.8+** dengan pustaka berikut:

| Pustaka | Fungsi |
| :--- | :--- |
| **matplotlib** | Menampilkan dan menggambar diagram visualisasi graf |
| **networkx** | Memodelkan struktur graf dependensi instruksi (*DiGraph*) |
| **scipy** | Algoritma kalkulasi posisi layout graf (*spring layout*) |
| **ipykernel** | Kernel untuk menjalankan notebook di VS Code / Jupyter |

### Cara Install Dependensi

Jalankan perintah berikut di terminal:

```bash
pip install -r requirements.txt
```

---

## 📁 Struktur Folder

```text
Data-Hazard/
├── ILP.ipynb           # Notebook utama (Simulasi ILP, Analisis Hazard, Register Renaming)
├── requirements.txt    # Daftar dependensi Python
├── .gitignore          # File ignore git untuk cache dan checkpoint
└── README.md           # Dokumentasi proyek
```

---

## 🚀 Cara Menjalankan

1. Buka file [`ILP.ipynb`](ILP.ipynb) di VS Code atau Jupyter Notebook.
2. Pastikan kernel Python yang dipilih sudah terpasang dependensi yang tercantum di atas.
3. Jalankan sel notebook:
   * **Cell 1**: Simulasi siklus ILP dasar (Perbandingan Sequential vs. Parallel Cycles).
   * **Cell 2**: Deteksi hazard komprehensif (RAW, WAR, WAW), proses *Register Renaming*, dan visualisasi grafik Sebelum vs. Sesudah Renaming.

---

## 💡 Ringkasan Hazard & Register Renaming

* **RAW**: Instruksi $B$ membaca register yang baru ditulis instruksi $A$. Wajib diselesaikan dengan *forwarding* atau *stall*.
* **WAR**: Instruksi $B$ menulis ke register yang sedang dibaca instruksi $A$. Merupakan *false dependency* karena hanya disebabkan oleh keterbatasan nama register.
* **Solusi Register Renaming**: Register target pada instruksi $B$ diubah ke register temporer (misal: `R2` $\rightarrow$ `R2_renamed1`). Hasilnya, ketergantungan WAR hilang dan instruksi dapat dijalankan secara bersamaan.
