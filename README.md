import time
from datetime import datetime, timedelta

class AltitudeMonitor:
    def __init__(self, threshold=2500):
        self.threshold = threshold
        self.start_time = None
        self.total_time = timedelta()
    
    def start_monitoring(self, altitude):
        if altitude >= self.threshold:
            if self.start_time is None:
                self.start_time = datetime.now()
                print(f"Начало отсчета: {self.start_time}")
            else:
                print("Уже в режиме кислородного голодания.")
        else:
            print(f"Высота {altitude} метров недостаточна для кислородного голодания.")
    
    def stop_monitoring(self):
        if self.start_time is not None:
            elapsed_time = datetime.now() - self.start_time
            self.total_time += elapsed_time
            print(f"Завершение отсчета. Прошедшее время: {elapsed_time}")
            self.start_time = None
        else:
            print("Отсчет времени не был запущен.")
    
    def get_total_time(self):
        return self.total_time

# Пример использования
monitor = AltitudeMonitor(threshold=2500)

# Начало мониторинга (предполагается, что высота в метрах поступает из внешнего источника)
monitor.start_monitoring(altitude=3000)
time.sleep(5)  # Эмуляция времени, проведенного на высоте
monitor.stop_monitoring()

# Получение общего времени в режиме кислородного голодания
print(f"Общее время в режиме кислородного голодания: {monitor.get_total_time()}")

