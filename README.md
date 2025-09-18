# 💻 FFT Architecture
> MATLAB 기반 Fixed Point 모델 설계와 SystemVerilog RTL 구현을 통해 512-point FFT를 설계 및 검증한 신호 처리 시스템입니다.  
> 8-radix FFT와 CBFP(Coefficient Block Floating Point) 알고리즘을 적용하여 연산 효율과 정밀도를 동시에 확보하였습니다.

---


# 📌 프로젝트 개요

| 항목             | 내용                                                   |
|------------------|--------------------------------------------------------|
| **⏱️ 개발 기간** | 2024.07.18 ~ 2024.08.01                               |
| **🖥️ 개발 환경**  | Vivado, VCS, VSCode                               |
| **💻 언어**       | System Verilog                                           |

---

# 🎯 설계 목표 (Front-end Process)

| 단계 | 내용 | 세부 사항 |
|------|------|-----------|
| **1) Spec. Analysis** | 사양 분석 | FFT 512pt, 입력 9bit |
| **2) Algorithm Search** | 알고리즘 탐색 | 8-radix FFT, CBFP 적용 |
| **3) Floating-point Modeling** | 부동소수점 모델링 | MATLAB 기반 FFT 구현 |
| **4) Fixed-point Modeling** | 고정소수점 모델링 | MATLAB `<3.6>` 포맷 변환 |
| **5) RTL Design (ASIC)** | RTL 설계 | SystemVerilog FFT 모듈 구현 및 검증 |
| **6) RTL Verification (FPGA)** | RTL 검증 | Vivado VIO 기반 데이터 merge |
| **7) Logic Synthesis** | 논리 합성 | Synthesis & Implementation (+Bitstream 생성) |

---

# ➕ Butterfly 연산 결과 검증 (MATLAB vs RTL Sim)

## 🆚 비교 개요
- **대상 모듈**: `module0~2` 내 각 버터플라이 연산 블록 (`bfly02`, `bfly12`, `bfly22`)
- **검증 항목**:
  - **cosine 입력 데이터(왼쪽 파형)**
  - **random 입력 데이터(오른쪽 파형)**
- **검증 방법**: MATLAB 참조 모델 결과 vs RTL 시뮬레이션 결과 비교 (Real/Imag)

## 1️⃣ bfly02 연산 결과
<img width="1500" alt="image" src="https://github.com/user-attachments/assets/f1f9f4a0-94c4-4ed1-9bda-d05cb5776e7b" />

## 2️⃣ bfly12 연산 결과
<img width="1500" alt="image" src="https://github.com/user-attachments/assets/8d7683ea-b89f-476d-9800-7df552efc727" />


## 3️⃣ bfly22 연산 결과
<img width="1500" alt="image" src="https://github.com/user-attachments/assets/d122e9e7-dbeb-4522-9a42-d78255f429cb" />

---

# ⚛️ Synthesis

## 1️⃣ Timing Report
- 전체 Top 기준 합성 결과 Slack이 **MET(충족)** 된 것을 확인할 수 있습니다.
<img width="1880" height="496" alt="image" src="https://github.com/user-attachments/assets/d37e7876-dd30-4be9-ad37-cec69aacb47b" />


## 2️⃣ Area
- 합성된 회로는 총 142470의 셀 면적을 가지는 것을 확인할 수 있습니다.
<img width="510" height="245" alt="image" src="https://github.com/user-attachments/assets/456a33cd-e5d9-44f9-91f8-28e04efb8209" />


---

# 🛠️ FPGA Synthesis

## 1️⃣ Timing Report
- FPGA 합성 결과 Slack이 **MET(충족)** 된 것을 확인할 수 있습니다.
<img width="534" height="183" alt="image" src="https://github.com/user-attachments/assets/55560bab-e552-4c66-92da-5d7a122dc585" />

## 2️⃣ Resource Utilization Report
- LUT 12.6%, FF 8.2%, DSP 12.3%로 전체 자원 대비 낮은 수준의 활용도를 보인 것을 알 수 있습니다.
<img width="550" height="503" alt="image" src="https://github.com/user-attachments/assets/e67088a5-001d-414d-a44a-a7d4a6df6a11" />
