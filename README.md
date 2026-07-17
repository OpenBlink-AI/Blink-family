# 👁️ Blink Model Family (Base & Instruct)

Oficiální repozitář pro rodinu modelů **Blink** od organizace **OpenBlink AI**. 

Blink je rodina ultra-kompaktních, vysoce efektivních jazykových modelů (Small Language Models) s otevřeným zdrojovým kódem. Jsou navrženy tak, aby běžely lokálně na běžném uživatelském hardwaru, minimalizovaly halucinace a dosahovaly maximální přesnosti skrze pokročilé systémy **RAG (Retrieval-Augmented Generation)**.

---

## 🗺️ Přehled modelů (Blink Tiers)

Rodina Blink se skládá ze tří specificky navržených úrovní. Každá úroveň odpovídá jinému hardwarovému a jazykovému zaměření:

| Model | Velikost | Primární jazyk | Doporučený hardware | Hlavní účel |
| :--- | :--- | :--- | :--- | :--- |
| **NanoBlink** | **6M** parametrů | Čeština (CZ) | Spotřebitelské GPU (např. RTX 3050 Laptop) | Lokální testování, porozumění české gramatice, rychlá extrakce z kontextu. |
| **TinyBlink** | **24M** parametrů | Angličtina (EN) | Bezplatný cloud / Slabší GPU (např. Tesla T4) | Plynulá konverzace, pokročilé filtrování informací z DuckDuckGo API. |
| **Blink** | **96M** parametrů | Bilingvní (CZ / EN) | Multi-GPU / Vyšší výkon (např. 2x T4 / RTX 3090) | Vlajková loď, přepínání jazyků, základy logického uvažování a encyklopedie. |

---

## ⚙️ Klíčové vlastnosti a architektura

Všechny modely řady Blink sdílejí pokročilé architektonické prvky, které z každého parametru mačkají absolutní maximum:

* **Architektura "Čisté Hlavy" (Context-First):** Modely záměrně neplýtvají kapacitou na ukládání statických encyklopedických dat. Jsou vytrénovány jako špičkové procesory kontextu – text čtou, filtrují a analyzují v reálném čase z dodaných zdrojů.
* **Grouped-Query Attention (GQA):** Optimalizovaný mechanismus pozornosti, který drasticky zmenšuje KV cache a umožňuje bleskové zpracování dlouhých textů z internetových vyhledávačů.
* **SwiGLU Activation & RoPE:** Moderní aktivace a rotační poziční embeddingy (vycházející z architektury Llama) zajišťují stabilitu a hlubší logické vazby v textu.
* **Vlastní Byte-Level BPE Tokenizéry:** Na míru natrénované slovníky (např. 12k pro češtinu), které zabraňují zbytečnému kouskování slov s diakritikou, šetří paměť a zrychlují inference.
* **Sdílení vah (Tie Word Embeddings):** Vstupní a výstupní vrstvy sdílejí váhy, což uvolňuje miliony parametrů pro samotné skryté vrstvy modelu.

---

## 🚀 Jak to funguje s RAGem?

Modely Blink jsou optimalizovány pro pipeline:
1. **Dotaz:** Uživatel položí otázku.
2. **Retrieval:** Python skript vyhledá relevantní a čerstvá data (např. přes DuckDuckGo).
3. **Prompt:** Data jsou zabalena do speciálních tokenů: `[CONTEXT] {vyhledaný_text} [QUESTION] {dotaz} [ANSWER]`.
4. **Generování:** Model Blink bleskově vygeneruje přesnou odpověď bez halucinací na základě poskytnutých důkazů.

---

## 📁 Struktura repozitáře

* `/configs` - Konfigurační soubory pro jednotlivé tiery (`config.json`).
* `/tokenizers` - Vlastní natrénované `.json` tokenizéry pro češtinu a angličtinu.
* `/scripts` - Kódy pro trénování, přípravu dat a integraci s DuckDuckGo vyhledáváním.

---

## 🛡️ Licence & Open-Source

Všechny modely a zdrojové kódy v rámci OpenBlink AI jsou vydány pod svobodnou licencí **MIT** (nebo Apache 2.0 - doplň podle sebe). Jsou plně self-hostable, bezplatné a bezpečné pro offline použití.
