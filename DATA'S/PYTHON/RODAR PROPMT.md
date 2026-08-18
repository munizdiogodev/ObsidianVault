
Caso voce tenha que trabalhar com questao de interface em seu código, mas o agendador de tarefas nao esta deixando, use isso:

e coloque no agendador de tarefas esse código

```python
import subprocess

import sys

import os

import time

  

# --- CONFIGURAÇÕES DE CAMINHOS ---

CAMINHO_RAIZ = r"\\10.0.0.99\toptherm\CONTROLDESK\MIS\Relação_Ponto_Funcionarios"

SCRIPTS = [

    os.path.join(CAMINHO_RAIZ, "Face_id.py")

]

  

def rodar_sequencia_direta():

    """Roda a sequência de robôs sem o intermediário do CMD/subprocess."""

    print("Iniciando a sequência de robôs...")

    for script_path in SCRIPTS:

        script_name = os.path.basename(script_path)

        print(f"\n--- INICIANDO: {script_name} ---")

        try:

            # Roda o script usando o interpretador Python atual (sys.executable)

            # Isso é mais limpo do que chamar 'python' + caminho do script.

            subprocess.run(

                [sys.executable, script_path],

                check=True,

                # IMPORTANTE: Não use capture_output=True, text=True ou shell=True aqui

                # para evitar que o subprocesso seja isolado do ambiente gráfico.

            )

            print(f"✅ {script_name} finalizado com sucesso.")

            time.sleep(5)

        except subprocess.CalledProcessError:

            print(f"❌ ERRO: O script {script_name} falhou. Interrompendo a sequência.")

            break

        except FileNotFoundError:

            print(f"❌ ERRO: O script {script_name} não foi encontrado.")

            break

        except Exception as e:

            print(f"❌ ERRO Inesperado ao rodar {script_name}: {e}")

            break

  

if __name__ == "__main__":

    rodar_sequencia_direta()

```