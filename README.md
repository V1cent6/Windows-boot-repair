# Windows Boot Recovery Guide


## Sobre(Português)
Este repositório contém um guia detalhado sobre como restaurar a inicialização do Windows em sistemas UEFI e Legacy BIOS. Se o teu sistema não arranca corretamente, podes seguir estes passos para reparar o boot.

## About(English)
This repository contains a detailed guide on how to restore Windows bootability on UEFI and Legacy BIOS systems. If your system does not boot properly, you can follow these steps to repair the boot.


## Aviso
**Usa estes comandos com cuidado!** Alterações incorretas no boot podem tornar o sistema inoperável. Certifica-te de que selecionas as partições corretas.

**Use these commands with caution!** Incorrect boot changes can render the system inoperable. Make sure you select the correct partitions.

Se não tens a certeza do que estás a fazer, recomendo que procure ajuda técnica antes de executar qualquer comando.

If you are unsure of what you are doing, I recommend seeking technical help before executing any commands.


Como Aceder ao Prompt de Comando do Windows(How to acess to Windows comands Prompt)

Para restaurar o boot, é preciso aceder ao Prompt de Comando através do ambiente de recuperação do Windows. Existem várias formas de o fazer:

To restore the boot, you need to access the Command Prompt through the Windows recovery environment. There are several ways to do this:

1️-Usando uma Pen USB Bootável com o Windows:
   Using a Bootable USB Pen with Windows:

   Se o teu sistema não arranca corretamente, podes utilizar um dispositivo USB com o Windows para       aceder ao Prompt de Comando:
   If your system does not boot correctly, you can use a USB device with Windows to access the          Command Prompt:

   Criar uma pen USB bootável com o Windows 10 ou 11:
   Create a bootable USB flash drive with Windows 10 or 11:

   Se não sabes qual o teu Windows (10 ou 11), usa um Windows 11 – funciona para ambos.
   If you don't know which Windows you have (10 or 11), use Windows 11 – it works for both.

   Para criares uma pe bootável podes usar ferramentas como rufus, ventoy..... .
   To create a bootable boot you can use tools like rufus, ventoy..... .

   Liga a pen ao computador e arranca a partir dela.
   Connect the pen to the computer and boot from it.

   No ecrã de instalação do Windows, clica em Reparar o computador.
   On the Windows installation screen, click Repair your computer.

   Vai a Solução de Problemas → Opções Avançadas → Prompt de Comando.
   Go to Troubleshooting → Advanced Options → Command Prompt.

2️-Se Não Tens uma Pen USB com o Windows:
   If you don't have a USB stick with Windows:

   Caso não tenhas uma pen USB, podes tentar;
   If you don't have a USB pen, you can try;

   Aceder ao Ambiente de Recuperação (WinRE);
   Access the Recovery Environment (WinRE);

   Liga o computador e assim que o logótipo do Windows for apresentado, mantem o botão de ligar          pressionado, repete o processo 3 vezes seguidas.
   Turn on the computer and as soon as the Windows logo appears, keep the power button pressed,          repeat the process 3 times in a row.

   Na 4ª tentativa, o Windows deve arrancar no Ambiente de Recuperação.
   On the 4th attempt, Windows should boot into the Recovery Environment.

   Vai a Solução de Problemas → Opções Avançadas → Prompt de Comando.
   Go to Troubleshooting → Advanced Options → Command Prompt.


## Como Restaurar o Boot do Windows (How to Restore Windows Boot)

### **Para UEFI BIOS(For UEFI BIOS):**
1. Abre o **Prompt de Comando** a partir de um ambiente de recuperação do Windows.
2. Executa os seguintes comandos:
   
1. Open **Command Prompt** from a Windows recovery environment.
2. Run the following commands:
   ```
   diskpart
   list disk
   select disk 0  # (ou outro número conforme necessário // or other number as required)
   list partition
   select partition X  # (tem que ser a partição do sistema, normalmente entre 100MB e 500MB // it has to be the system partition, usually between 100MB and 500MB)
   assign letter=S:
   exit
   ```
4. Agora recria os ficheiros de boot(Now recreate the boot files):
   
   ```
   bcdboot C:\Windows /s S: /f UEFI
   ```
   > **Nota:** Após veres a mensagem confirmando que os ficheiros de boot foram criados com sucesso, continua para o próximo passo.
   
   > **Note:** After you see the message confirming that the boot files were created successfully, continue to the next step.

5. Remove a letra da partição(Remove the letter from the partition:
   
   ```
   diskpart
   list disk
   select disk 0
   list partition
   select partition X
   remove letter=S
   exit
   ```


### **Para Legacy BIOS (MBR):**
1. No ambiente de recuperação do Windows, abre o **Prompt de Comando**.
2. Executa os seguintes comandos:

1. In the Windows recovery environment, open the **Command Prompt**.
2. Run the following commands:
   
   ```
   bootrec /fixmbr
   bootrec /fixboot
   bootrec /scanos
   bootrec /rebuildbcd
   ```
4. Reinicia o computador e verifica se o problema foi resolvido (Reboot your computer and check if the problem is resolved).




