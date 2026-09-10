# AF1
Atividade da Faculdade (Desenvolvimento de dispositivos moveis)
// =========================================================================
// Avaliação Formativa I - Programação para Dispositivos Móveis
// Sistema de Emissão de Passagens SkyHorizon Airlines
// =========================================================================

// -------------------------------------------------------------------------
// Exercício 1: Abstração e Classes de Apoio
// -------------------------------------------------------------------------
class Passageiro {
  String? nome;
  String? cpf;
  String? rg;
  String? email;
  String? celular;

  Passageiro({this.nome, this.cpf, this.rg, this.email, this.celular});
}

class PlataformaVenda {
  int? codigoCanal;
  String? nomeCanal;

  PlataformaVenda({this.codigoCanal, this.nomeCanal});
}

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

// -------------------------------------------------------------------------
// Exercícios 2 a 7: Classe Passagem
// -------------------------------------------------------------------------
class Passagem {
  // Exercício 5: atributo privado
  String? _codigoLocalizador = '';

  // Exercício 2: atributos agregados
  Passageiro? passageiro;
  PlataformaVenda? plataforma;
  Atendente? atendente;
  String? observacoes;

  // Exercício 2: Construtor Não Nomeado
  Passagem() {}

  // Exercício 3: Construtores Nomeados
  Passagem.somenteCodigo(String codigoLocalizador)
      : _codigoLocalizador = codigoLocalizador;

  Passagem.completa(
    String codigoLocalizador,
    Passageiro? passageiro,
    PlataformaVenda? plataforma,
    Atendente? atendente,
    String? observacoes,
  )   : _codigoLocalizador = codigoLocalizador,
        passageiro = passageiro,
        plataforma = plataforma,
        atendente = atendente,
        observacoes = observacoes;

  // Exercício 4: Construtores Nomeados com Parâmetros Nomeados
  Passagem.codigoEPassageiro({String? codigoLocalizador, this.passageiro})
      : _codigoLocalizador = codigoLocalizador;

  Passagem.all(
    String codigoLocalizador, {
    required Passageiro? passageiro,
    required PlataformaVenda? plataforma,
    required Atendente? atendente,
    String? observacoes,
  })  : _codigoLocalizador = codigoLocalizador,
        passageiro = passageiro,
        plataforma = plataforma,
        atendente = atendente,
        observacoes = observacoes;

  // Exercício 5: getter e setter tradicionais (métodos)
  String? getCodigoLocalizador() {
    return _codigoLocalizador;
  }

  void setCodigoLocalizador(String? codigoLocalizador) {
    if (codigoLocalizador == null || codigoLocalizador.isEmpty) {
      print("Código localizador de passagem inválido!");
      return;
    }
    _codigoLocalizador = codigoLocalizador;
  }

  // Exercício 6: getter e setter nativos do Dart
  String? get codigoLocalizador => _codigoLocalizador;

  set codigoLocalizador(String? codigoLocalizador) {
    if (codigoLocalizador == null || codigoLocalizador.isEmpty) {
      print("Código localizador de passagem inválido!");
      return;
    }
    _codigoLocalizador = codigoLocalizador;
  }

  // Exercício 7: métodos de negócio
  void EmitirPassagem() {
    print("Passagem emitida com sucesso!");
  }

  bool CancelarPassagem() {
    print("Passagem cancelada com sucesso!");
    return true;
  }

  void AtualizarPassagem() {
    print("Passagem atualizada com sucesso!");
  }

  Passagem ConsultarPassagem(String codigo) {
    print("Passagem consultada com sucesso!");
    return Passagem();
  }
}

// -------------------------------------------------------------------------
// Exercício 9: Mixins de Log e Auditoria
// -------------------------------------------------------------------------
mixin Logger {
  void log(String mensagem) {
    print(mensagem);
  }
}

mixin Auditoria {
  void auditar(String mensagem) {
    print("[Auditoria]: $mensagem");
  }
}

// -------------------------------------------------------------------------
// Exercício 8 e 9: Herança + Mixins
// -------------------------------------------------------------------------
class PassagemPrimeiraClasse extends Passagem with Logger, Auditoria {
  String? loungeAcesso;

  PassagemPrimeiraClasse(
    String codigoLocalizador, {
    Passageiro? passageiro,
    PlataformaVenda? plataforma,
    Atendente? atendente,
    String? observacoes,
    required this.loungeAcesso,
  }) : super.all(
          codigoLocalizador,
          passageiro: passageiro,
          plataforma: plataforma,
          atendente: atendente,
          observacoes: observacoes,
        );

  // Exercício 10: Sobrescrita polimórfica
  @override
  void AtualizarPassagem() {
    print("Passagem de Primeira Classe atualizada com sucesso!");
    log("Alteração realizada pelo atendente: ${super.atendente?.nome}");
    auditar("Verificação de segurança realizada para a Primeira Classe.");
  }
}

// -------------------------------------------------------------------------
// Exercício 10: Função main() de demonstração
// -------------------------------------------------------------------------
void main() {
  print("========== SISTEMA SKYHORIZON AIRLINES ==========\n");

  // Objetos de apoio
  Passageiro passageiro1 = Passageiro(
    nome: "Maria Silva",
    cpf: "123.456.789-00",
    rg: "12.345.678-9",
    email: "maria.silva@email.com",
    celular: "(11) 91234-5678",
  );

  PlataformaVenda plataforma1 = PlataformaVenda(
    codigoCanal: 1,
    nomeCanal: "Site Oficial",
  );

  Atendente atendente1 = Atendente(
    nome: "João Souza",
    matricula: "AT-2024",
    cargo: "Atendente de Balcão",
    email: "joao.souza@skyhorizon.com",
    celular: "(11) 98888-1111",
    salario: 3500.00,
  );

  // ---- 1) Passagem padrão (construtor não nomeado + setter nativo) ----
  print("--- Passagem Padrão (construtor vazio) ---");
  Passagem passagemPadrao = Passagem();
  passagemPadrao.codigoLocalizador = "SKH1001"; // usa o set nativo (Ex.6)
  passagemPadrao.passageiro = passageiro1;
  passagemPadrao.plataforma = plataforma1;
  passagemPadrao.atendente = atendente1;
  passagemPadrao.observacoes = "Passageiro preferencial.";

  print("Código: ${passagemPadrao.codigoLocalizador}");
  passagemPadrao.EmitirPassagem();
  passagemPadrao.AtualizarPassagem();

  // Testando validação do setter (Exercício 5/6)
  passagemPadrao.setCodigoLocalizador(""); // deve exibir mensagem de erro
  print("");

  // ---- 2) Passagem padrão usando construtor all() com nomeados ----
  print("--- Passagem criada com Passagem.all() ---");
  Passagem passagemAll = Passagem.all(
    "SKH2002",
    passageiro: passageiro1,
    plataforma: plataforma1,
    atendente: atendente1,
    observacoes: "Bagagem extra despachada.",
  );

  print("Código: ${passagemAll.getCodigoLocalizador()}");
  print("Passageiro: ${passagemAll.passageiro?.nome}");
  passagemAll.EmitirPassagem();
  bool cancelada = passagemAll.CancelarPassagem();
  print("Passagem cancelada? $cancelada");
  print("");

  // ---- 3) Passagem de Primeira Classe (herança + mixins) ----
  print("--- Passagem de Primeira Classe ---");
  PassagemPrimeiraClasse passagemVip = PassagemPrimeiraClasse(
    "SKH3003",
    passageiro: passageiro1,
    plataforma: plataforma1,
    atendente: atendente1,
    observacoes: "Cliente Diamond.",
    loungeAcesso: "Lounge Internacional - Terminal 3",
  );

  print("Código: ${passagemVip.codigoLocalizador}");
  print("Lounge de acesso: ${passagemVip.loungeAcesso}");
  passagemVip.EmitirPassagem();

  // Chamada polimórfica: executa a versão sobrescrita (Exercício 10)
  passagemVip.AtualizarPassagem();

  // Uso direto dos mixins (Exercício 9)
  passagemVip.log("Log manual: passagem VIP validada em sistema.");
  passagemVip.auditar("Auditoria manual concluída sem pendências.");

  print("\n========== FIM DA DEMONSTRAÇÃO ==========");
}
