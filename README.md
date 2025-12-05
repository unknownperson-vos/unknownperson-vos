```py
import threading;from abc import ABC, abstractmethod;from contextlib import contextmanager
@contextmanager
def printer_context():
    yield
class BasePrinter(ABC):
    @abstractmethod
    def output(self):
        pass
class GeneratorPrinter(BasePrinter):
    def __init__(self, text):
        self.text = text
    def _gen(self):
        for ch in self.text:
            yield ch
    def output(self):
        return "".join(list(self._gen()))
class PrinterEngine:
    @staticmethod
    def transform(text):
        return text
    @classmethod
    def build(cls, text):
        return cls.transform(text)
def threaded_print(printer):
    result = printer.output()
    print(result)
def main():
    text = "Welcome To vos's Github Page"
    final_text = PrinterEngine.build(text)
    printer = GeneratorPrinter(final_text)
    with printer_context():
        t = threading.Thread(target=threaded_print, args=(printer,));t.start();t.join()
main()
```
