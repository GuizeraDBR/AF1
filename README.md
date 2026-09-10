```dart
// Avaliação Formativa I
// Programação para Dispositivos Móveis
// Sistema de Emissão de Passagens - SkyHorizon Airlines

// Classe Passageiro
class Passageiro {
  String? nome;
  String? cpf;
  String? rg;
  String? email;
  String? celular;

  Passageiro({
    this.nome,
    this.cpf,
    this.rg,
    this.email,
    this.celular,
  });
}

// Classe Plataforma de Venda
class PlataformaVenda {
  int? codigoCanal;
  String? nomeCanal;

  PlataformaVenda({
    this.codigoCanal,
    this.nomeCanal,
  });
}

// Classe Atendente
class Atendente {
  String? nome;
  String? matricula;
  String? cargo;
  String? email;
  String? celular;
  double? salario;

  Atendente({
    this.nome,
    this.matricula,
    this.cargo,
    this.email,
    this.celular,
    this.salario,
  });
}

// Classe principal Passagem
class Passagem {
  // Atributo privado
  String? _codigoLocalizador;

  // Objetos agregados
  Passageiro? passageiro;
  PlataformaVenda? plataforma;
  Atendente? atendente;
  String? observacoes;

  // Construtor padrão
  Passagem();

  // Construtor nomeado
  Passagem.somenteCodigo(String codigo)
      : _codigoLocalizador = codigo;

  // Construtor completo
  Passagem.completa(
    String codigo,
    this.passageiro,
    this.plataforma,
    this.atendente,
    this.observacoes,
  ) : _codigoLocalizador = codigo;

  // Construtor com parâmetros nomeados
  Passagem.codigoEPassageiro({
    String? codigo,
    this.passageiro,
  }) : _codigoLocalizador = codigo;

  // Construtor completo com parâmetros nomeados
  Passagem.all(
    String codigo, {
    this.passageiro,
    this.plataforma,
    this.atendente,
    this.observacoes,
  }) : _codigoLocalizador = codigo;

  // Getter tradicional
  String? getCodigoLocalizador() {
    return _codigoLocalizador;
  }

  // Setter tradicional
  void setCodigoLocalizador(String codigo) {
    if (codigo.isEmpty) {
      print("Código inválido!");
      return;
    }

    _codigoLocalizador = codigo;
  }

  // Getter nativo
  String? get codigoLocalizador => _codigoLocalizador;

  // Setter nativo
  set codigoLocalizador(String codigo) {
    if (codigo.isEmpty) {
      print("Código inválido!");
      return;
    }

    _codigoLocalizador = codigo;
  }

  // Métodos de negócio
  void emitirPassagem() {
    print("Passagem emitida com sucesso!");
  }

  bool cancelarPassagem() {
    print("Passagem cancelada com sucesso!");
    return true;
  }

  void atualizarPassagem() {
    print("Passagem atualizada com sucesso!");
  }

  Passagem consultarPassagem(String codigo) {
    print("Passagem consultada: $codigo");
    return Passagem();
  }
}

// Mixin para registrar logs
mixin Logger {
  void log(String mensagem) {
    print("Log: $mensagem");
  }
}

// Mixin para auditoria
mixin Auditoria {
  void auditar(String mensagem) {
    print("Auditoria: $mensagem");
  }
}

// Herança + Mixins
class PassagemPrimeiraClasse extends Passagem
    with Logger, Auditoria {

  String? loungeAcesso;

  PassagemPrimeiraClasse(
    String codigo, {
    this.loungeAcesso,
    super.passageiro,
    super.plataforma,
    super.atendente,
    super.observacoes,
  }) : super.all(codigo);

  // Sobrescrita do método
  @override
  void atualizarPassagem() {
    print("Passagem de Primeira Classe atualizada!");

    log("Alteração realizada pelo atendente: ${atendente?.nome}");

    auditar(
      "Verificação de segurança realizada para Primeira Classe.",
    );
  }
}

void main() {
  print("===== SKYHORIZON AIRLINES =====");

  // Criando um passageiro
  Passageiro passageiro = Passageiro(
    nome: "Maria Silva",
    cpf: "123.456.789-00",
    email: "maria@email.com",
    celular: "(11) 99999-9999",
  );

  // Criando uma plataforma de venda
  PlataformaVenda plataforma = PlataformaVenda(
    codigoCanal: 1,
    nomeCanal: "Site Oficial",
  );

  // Criando um atendente
  Atendente atendente = Atendente(
    nome: "João Souza",
    matricula: "AT-2024",
    cargo: "Atendente",
    salario: 3500,
  );

  // Criando uma passagem
  Passagem passagem = Passagem();

  passagem.codigoLocalizador = "SKH1001";
  passagem.passageiro = passageiro;
  passagem.plataforma = plataforma;
  passagem.atendente = atendente;
  passagem.observacoes = "Passageiro preferencial.";

  print("\n--- Passagem ---");
  print("Código: ${passagem.codigoLocalizador}");
  print("Passageiro: ${passagem.passageiro?.nome}");

  passagem.emitirPassagem();
  passagem.atualizarPassagem();

  // Criando passagem usando construtor nomeado
  Passagem passagem2 = Passagem.all(
    "SKH2002",
    passageiro: passageiro,
    plataforma: plataforma,
    atendente: atendente,
    observacoes: "Bagagem extra.",
  );

  print("\n--- Outra Passagem ---");
  print("Código: ${passagem2.getCodigoLocalizador()}");

  passagem2.emitirPassagem();
  passagem2.cancelarPassagem();

  // Criando passagem de primeira classe
  PassagemPrimeiraClasse passagemVip =
      PassagemPrimeiraClasse(
    "SKH3003",
    passageiro: passageiro,
    plataforma: plataforma,
    atendente: atendente,
    loungeAcesso: "Lounge Internacional",
  );

  print("\n--- Primeira Classe ---");
  print("Código: ${passagemVip.codigoLocalizador}");
  print("Lounge: ${passagemVip.loungeAcesso}");

  passagemVip.emitirPassagem();

  // Polimorfismo
  passagemVip.atualizarPassagem();

  // Utilizando os mixins
  passagemVip.log("Passagem VIP validada.");
  passagemVip.auditar("Auditoria concluída.");

  print("\n===== FIM =====");
}
```
