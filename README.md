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




