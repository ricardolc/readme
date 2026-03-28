Coverage em Python
 ```
# pip install coverage
# coverage run -m unittest tests/unitarios/test_operacoes_matematicas.py && coverage report

# quando tem muitos testes, é melhor usar discover para rodar todos os testes de uma vez
# coverage run -m unittest discover tests/unitarios && coverage report

# obtendo o relatório de cobertura para um teste específico
# python -m coverage report

# em html
# coverage html
 ```
