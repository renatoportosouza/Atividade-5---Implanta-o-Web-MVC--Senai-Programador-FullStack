# Atividade 5 - Implantação Web MVC

## Descrição
A clinica veterinaria **LH-Pet** solicitou o desenvolvimento de um projeto Web **.NET** com arquitetura **MVC**. Inicialmente, a aplicação não terá banco de dados, mas futuramente a empresa migrara toda a sua base de dados para o novo sistema.

Este projeto visa iniciar a estruturação de uma aplicação web **.NET MVC**, criar os primeiros **models (Cliente e Fornecedor)**, instanciá-los no **controller (HomeController)** e exibi-los na **view (Index.cshtml)**.

---
## Estrutura MVC
O **MVC** (“Model-View-Controller”) e um padrão de arquitetura de software organizado em camadas. Sua aplicação será dividida em:

- **Model**: Responsável pela implementação dos dados e suas manipulações.
- **View**: Responsável pela interface gráfica apresentada ao usuário.
- **Controller**: Responsável pela lógica de negócios do sistema, coordenando Models e Views.

---
## Configuração do Ambiente
Antes de iniciar, verifique a versão do **.NET** instalada no seu computador executando o seguinte comando no terminal:

```sh
 dotnet --version
```

Para este projeto, utilizamos a versão **.NET 7.0**.

---
## Criação do Projeto MVC
1. Abra o terminal (cmd) e crie um novo projeto MVC:
   ```sh
   dotnet new mvc -o LHPet
   ```

2. Acesse a pasta do projeto:
   ```sh
   cd LHPet
   ```

3. Execute o projeto para testar se esta funcionando:
   ```sh
   dotnet run
   ```

4. Acesse o link gerado no navegador para conferir.
5. Para parar a aplicação, use **Ctrl + C**.

---
## Configuração dos Models
1. No **Visual Studio Code**, crie a pasta `Models`, caso não exista.
2. Crie um arquivo chamado `Cliente.cs` e adicione o seguinte código:

   ```csharp
   namespace LHPet.Models;
   public class Cliente
   {
       public int Id { get; set; }
       public string Nome { get; set; }
       public string Cpf { get; set; }
       public string Email { get; set; }
       public string Paciente { get; set; }

       public Cliente(int id, string nome, string cpf, string email, string paciente)
       {
           this.Id = id;
           this.Nome = nome;
           this.Cpf = cpf;
           this.Email = email;
           this.Paciente = paciente;
       }
   }
   ```

3. Crie um arquivo chamado `Fornecedor.cs` e adicione o seguinte código:

   ```csharp
   namespace LHPet.Models;
   public class Fornecedor
   {
       public int Id { get; set; }
       public string Nome { get; set; }
       public string Cnpj { get; set; }
       public string Email { get; set; }

       public Fornecedor(int id, string nome, string cnpj, string email)
       {
           this.Id = id;
           this.Nome = nome;
           this.Cnpj = cnpj;
           this.Email = email;
       }
   }
   ```

---
## Configuração do Controller
1. No **Visual Studio Code**, localize e abra o arquivo `HomeController.cs` dentro da pasta `Controllers`.
2. Adicione as seguintes instâncias de `Cliente` e `Fornecedor`:

   ```csharp
   using Microsoft.AspNetCore.Mvc;
   using LHPet.Models;
   
   namespace LHPet.Controllers;
   public class HomeController : Controller
   {
       public IActionResult Index()
       {
           List<Cliente> listaClientes = new List<Cliente>
           {
               new Cliente(01, "Arthur A. Ferreira", "857.032.950-41", "arthur.antunes@sp.senai.br", "Madruga"),
               new Cliente(02, "William Henry Gates III", "039.618.250-09", "bill@microsoft.com", "Bug"),
               new Cliente(03, "Ada Lovelace", "800.777.920-50", "ada@ada.language.com", "Byron"),
               new Cliente(04, "Linus Torvalds", "933.622.400-03", "torvalds@osdl.org", "Pinguim"),
               new Cliente(05, "Grace Hopper", "911.702.988-00", "grace.hopper@cobol.com", "Loboc")
           };
           
           List<Fornecedor> listaFornecedores = new List<Fornecedor>
           {
               new Fornecedor(01, "C# PET S/A", "14.182.102/0001-80", "c-sharp@pet.org"),
               new Fornecedor(02, "Ctrl Alt Dog", "15.836.698/0001-57", "ctrl@alt.dog.br"),
               new Fornecedor(03, "BootsPet INC", "40.810.224/0001-83", "boots.pet@gatomania.us"),
               new Fornecedor(04, "Tik Tok Dogs", "87.945.350/0001-09", "noisnamidia@tiktokdogs.uk"),
               new Fornecedor(05, "Bifinho Forever", "18.760.614/0001-37", "contato@bff.us")
           };
           
           ViewBag.listaClientes = listaClientes;
           ViewBag.listaFornecedores = listaFornecedores;
           return View();
       }
   }
   ```

---
## Configuração da View
1. No **Visual Studio Code**, localize a pasta `Views > Home` e abra o arquivo `Index.cshtml`.
2. Adicione o seguinte código para exibir a **lista de Clientes**:

   ```html
   <table class="table table-hover">
       <caption>Lista de Clientes</caption>
       <thead>
           <tr>
               <th>Id</th>
               <th>Nome</th>
               <th>CPF</th>
               <th>Email</th>
               <th>Paciente</th>
           </tr>
       </thead>
       <tbody>
           @foreach (var item in @ViewBag.listaClientes)
           {
               <tr>
                   <td>@item.Id</td>
                   <td>@item.Nome</td>
                   <td>@item.Cpf</td>
                   <td>@item.Email</td>
                   <td>@item.Paciente</td>
               </tr>
           }
       </tbody>
   </table>
   ```

3. Adicione o seguinte código para exibir a **lista de Fornecedores**:

   ```html
   <table class="table table-hover">
       <caption>Lista de Fornecedores</caption>
       <thead>
           <tr>
               <th>Id</th>
               <th>Nome</th>
               <th>CNPJ</th>
               <th>Email</th>
           </tr>
       </thead>
       <tbody>
           @foreach (var item in @ViewBag.listaFornecedores)
           {
               <tr>
                   <td>@item.Id</td>
                   <td>@item.Nome</td>
                   <td>@item.Cnpj</td>
                   <td>@item.Email</td>
               </tr>
           }
       </tbody>
   </table>
   ```

---
## Executando a Aplicação
Para testar a aplicacao, execute:
```sh
dotnet run
```
Acesse o link gerado no navegador e confira a exibicao das listas de Clientes e Fornecedores.

