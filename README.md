# ESL-Image-Classification-on-FPGA
## Grupa nr. 3: Kamil Skałka, Krzysztof Garbicz, Stanisław Kusiak

**[Colab link](https://colab.research.google.com/drive/1_8cmjbcTBNUtGTsEJXET9WUd2Z2nKjwC?usp=sharing)**

Założenia treningu:
### **Dane**
- Zbiór: **CIFAR-10**
- Liczba obrazów:
    - **50 000** – trening
    - **10 000** – test
- Liczba klas: **10**
- Oryginalny rozmiar obrazka: **32 × 32 × 3 (RGB)**

### **Transformacje danych (train)**

1. **RandomHorizontalFlip** – losowe odbicie poziome (augmentacja)
2. **Resize(224×224)** – powiększenie obrazu do wymaganego wejścia MobileNetV2 (interpolacja)
3. **ToTensor()** – zamiana pikseli na tensory, skala 0–1
4. **Normalize(mean, std)** – normalizacja z wartościami CIFAR-10

### **Model**

- Architektura: **MobileNetV2**
- Wagi startowe: **IMAGENET1K_V1 (pretrained)**
- Modyfikacja:
    - Zmieniona ostatnia warstwa (`classifier[1]`) na **10 wyjść** (10 klas CIFAR-10)

### **Konfiguracja treningu**

- `batch_size = 128`
- Funkcja straty: **CrossEntropyLoss**
- Optymalizator: **Adam**, `lr = 1e-3`
- Akcelerator: **GPU (Tesla T4 – Colab)**
- Liczba epok: **5** (na start)

### **Wynik treningu**

- Zapis wag modelu: **`.pth`**
- Eksport do formatu **ONNX**:
    
    **`mobilenetv2_cifar10.onnx`**