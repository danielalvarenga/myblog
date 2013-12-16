Aprendendendo Rails
==

Como aplicação de exemplo vamos criar um Blog, que é muito útil para quem quer mostrar seu trabalho e agrega bastante valor ao profissional (quando tem conteúdo e o mesmo é de qualidade é claro). E o mesmo projeto pode ser utilizado para construir um site institucional (com as devidas adaptações... =P).

Utilizaremos Ruby 2 e Rails 4.

Criar uma Gemset chamada "blogs" com Ruby 2.0.0 e instalar a gem "rails":

	$ rvm use ruby-2.0.0@blogs --create
	$ gem install rails

Criar o projeto, que chamaremos de myblog:

	$ rails new myblog

Esse comando irá criar a pasta do projeto e instalará as gems necessárias a um projeto rails que estão listadas no arquivo "Gemfile" dentro do projeto.

Inicie o servidor web e depois acesse http://localhost:3000 para testar se sua aplicação está funcionando:

	$rails server # para finalizar utilize "Ctrl+C"

Conhecer e saber quais gems utilizar é a parte que considero mais complicada no aprendizado, mas com o tempo você pega as manhas! =)
Vamos adicionar algumas gems mais utilizadas pela comunidade.

Adicionar gems no final do arquivo "myblog/Gemfile":

	# Autenticação de Usuário
	gem 'devise'
	# Estrutura de configuração
	gem 'figaro'
	# Criar formulários mais fácil
	gem 'simple_form'
	# Para páginas estáticas .html.erb
	gem 'high_voltage'

	group :development do
	  # ajuda quando as coisas dão errado
	  gem 'better_errors'
	  # suprime as mensagens de distração no log
	  gem 'quiet_assets'
	  # gera arquivos para um layout de aplicação
	  gem 'rails_layout'
	end

	group :development, :test do
		# instancia objetos para serem utilizados nos testes
		gem "factory_girl_rails", "~> 4.3.0"
		# gem de testes
		gem 'rspec-rails', '~> 2.14.0'
	end

	group :test do
		# reduz a quantidade de código para testes mais simples, como testes de validação
		gem 'shoulda-matchers'
		# limpa a base de dados de teste após execultar os testes
		gem 'database_cleaner'
	end

Instalar no gemset as gems adicionadas ao projeto:

	$ bundle install

Ainda não veremos testes nesse tutorial, mas considero importante instalar as gems para a estrutura de testes ir sendo criada automáticamente conforme vamos criando nossa aplicação.

Instale a gem de testes BDD "RSpec" no projeto:

	$ rails generate rspec:install

Com isso você verá pastas e arquivos serem criados pelas gems factory-girl e rspec na pasta "myblog/spec" sempre que criar um novo model ou controller, mas não trabalharemos com testes ainda. Vamos pular essa parte e continuar.

Instale a gem de configuração no projeto:

	$ rails generate figaro:install

Será criado o arquivo "myblog/config/application.yml", onde você poderá criar "Variáveis de Ambiente" que poderão ser utilizadas em qualquer parte do projeto e normalmente utilizadas para armazenar logins e senha de banco de dados e de outras aplicações que talvez você possa integrar ao projeto futuramente. Como estas informações não devem ser commitadas para repositórios, esse arquivo é adicionado ao ".gitignore" automáticamente.

Então vamos adicionar algumas variáveis ao final do arquivo "myblog/config/application.yml" como exemplo:
	
	EMAIL_USERNAME: Your_Username # seu login
	EMAIL_PASSWORD: Your_Password # sua senha
	DOMAIN_NAME: example.com
	OWNER_EMAIL: me@example.com

Para podermos enviar e-mail através de nossa aplicação adicione o código abaixo ao final do arquivo "myblog/config/environments/development.rb" antes da palavra "end" (utilizaremos Gmail neste exemplo):
	
	# Configuração de acesso ao servidor de e-mail
	config.action_mailer.smtp_settings = {
	    address: "smtp.gmail.com",
	    port: 587,
	    domain: ENV["DOMAIN_NAME"],
	    authentication: "plain",
	    enable_starttls_auto: true,
	    user_name: ENV["EMAIL_USERNAME"],
	    password: ENV["EMAIL_PASSWORD"]
	}

	# Permite enviar e-mails em ambiente de desenvolvimento
	config.action_mailer.perform_deliveries = true

Agora nossa aplicação já está bem estruturada para darmos início ao desenvolvimento, então crie um repositório no GitHub com o mesmo nome do projeto e vamos fazer nosso primeiro commit:

	$ git init
	$ git add -A
	$ git commit -m "Commit Inicial"
	$ git remote add origin https://github.com/SEU_PERFIL_GITHUB/myblog.git
	$ git push -u origin master




