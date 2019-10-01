# Validation-failed-for-one-or-more-entities.-See-EntityValidationError


Exemplo para rastrear erros de Property de objetos e detalhar essa matriz no Visual studio durante a depuração. Mas você também pode capturar a exceção e gravar os erros em algum armazenamento de log ou no console:
EntityValidationErrors: é uma coleção que representa as entidades que não puderam ser validadas com êxito e a coleção interna. O EntityValidationErrors por entidade é uma lista de erros ha nível de propriedade.
 
 Essas mensagens de validação geralmente são úteis o suficiente para encontrar a fonte do problema
 #O valor da propriedade incorreta pode ser incluído no loop interno da seguinte maneira:
 
   [0] Existem varias formas para rastrear erros de propiedades obrigatorias,
   
   1) -  
 #imgiurl: https://imgbbb.com/image/LR5pyF

----------------- code-----------------------------
  private static void Main(string[] args)
        {
            try
            {
                using (var ctx = new Context())
                {
                    var estudante = new alunos()
                    {
                        nome = "joaoAfonso",
                        /*
                         * O CAMPO E-AMIL, FOI SETADO COMO [Required].
                         */
                        //email ="email@gmail.com"
                        fone = "8578785",
                        cpf = "15215855-20",
                        idCursos = 1,
                        IdInstrutores = 1
                    };

                    ctx.alunos.Include("cursos");
                    ctx.alunos.Include("instrutores");
                    ctx.alunos.Add(estudante);

                    ctx.SaveChanges();
                }
                Console.WriteLine("Dados Inseridos");
                Console.ReadLine();
            }
            catch (DbEntityValidationException e)
            {
                foreach (var eve in e.EntityValidationErrors)
                    foreach (var ve in eve.ValidationErrors)
                    {
                        Console.WriteLine("Property: \"{0}\", Value: \"{1}\", Error: \"{2}\"",
                            ve.PropertyName,
                            eve.Entry.CurrentValues.GetValue<object>(ve.PropertyName),
                            ve.ErrorMessage);
                    }
                throw;
            }


        }
        
        
       2)- Basta adicionar a seguinte expressão em uma janela do Quick Watch ou no mmediate window do propip visual studio o seguinte comando.
((System.Data.Entity.Validation.DbEntityValidationException)$exception).EntityValidationErrors

    No meu caso, veja como sou capaz de expandir para ValidationErrors List dentro da EntityValidationErrorscolections (img)
    url-igm - https://imgbbb.com/image/LR5UUC
        
 
