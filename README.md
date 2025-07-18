# 🎯 Хочешь следить за загрузкой своей GPU прямо из Python?

Вот простой скрипт, который показывает текущую загрузку видеокарты NVIDIA (через `nvidia-smi`). Подходит для мониторинга в ML-задачах, инференсе и просто для интереса.

### 📦 Зависимости: установленный nvidia-smi и Python 3.6+

### 🧠 Код:
```Python

import subprocess

def get_gpu_utilization():
    try:
        result = subprocess.check_output(
            ['nvidia-smi', '--query-gpu=utilization.gpu,memory.used,memory.total',
             '--format=csv,nounits,noheader'],
            encoding='utf-8'
        )
        lines = result.strip().split('\n')
        for idx, line in enumerate(lines):
            gpu_util, mem_used, mem_total = map(str.strip, line.split(','))
            print(f"🖥 GPU {idx}: {gpu_util}% load | {mem_used} MiB / {mem_total} MiB")
    except FileNotFoundError:
        print("❌ nvidia-smi not found. Make sure NVIDIA drivers are installed.")
    except Exception as e:
        print(f"⚠️ Error: {e}")

get_gpu_utilization()

```

#### 📊 Вывод будет примерно такой:
```
GPU 0: 23% load | 412 MiB / 8192 MiB
```
## 🔥 Советы:
- Можно запускать в цикле для live-мониторинга
- Легко интегрировать в Telegram-бота или Slack-уведомления
- Работает на всех машинах с установленным NVIDIA драйвером и nvidia-smi
