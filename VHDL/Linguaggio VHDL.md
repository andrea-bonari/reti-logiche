>[!note]
>VHDL (VHSIC Hardware Description Language) è un Hardware Description Language (HDL) ed è utilizzato per simulare e sintetizzare i circuiti logici. È un derivato del linguaggio Ada. La specifica del linguaggio VHDL è mantenuta da IEEE tramite lo standard IEEE 107.
>
>VHDL consente di modellare circuiti logici tramite una descrizione algoritmica, tramite una descrizione basata su formule logiche, oppure tramite una descrizione delle singole porte e interconnessioni.

L'estensione del file VHDL è `.vhd`. Il linguaggio è case-insensitive e fortemente tipizzato. Similmente al C, ogni "statement" è terminato con un punto e virgola. I commenti sono solo a riga singola e sono introdotti da `--`.

Un progetto VHDL può contenere:
- Dichiarazione di entità
- Descrizione dell'architettura di entità
- Dichiarazione di package
- Descrizione del contenuto di un package
- Configurazioni

### Entità
>[!note]
>L'entità è il concetto base di VHDL e rappresenta, in maniera astratte, un'interfaccia con una visione "ai morsetti", quindi non fornisce alcuna descrizione del suo comportamento.
>
>```vhdl
>entity componente is
>	port (a, b, c : in std_logic;
>		  d, e    : out std_logic);
>end;
>```

In VHDL, i tipi di dato si trovano in vari package, i principali sono
- `standard`
- `std_logic_1164`
- `numeric_std`
- `float_std`

>[!tip] Libreria `standard`
>La libreria standard contiene tipi di dati scalari, come `bit`, `boolean`, `integer`, `real`, `time` o `character`, oppure dati vettoriali, come `bit_vector` o `string`.
>
>Esistono anche le enumerazioni, che contengono un insieme finito di possibili valori:
>```vhdl
>type color is (black, red, green, blue);
>```
>
>Inoltre esistono array:
>```vhdl
>type each_month is array(1 to 12) integer;
>```
>
>E record: 
>```vhdl
>type studente is
>record
>	nome      : string (1 to 6);
>	cognome   : string (1 to 6);
>	matricola : integer;
>end record;
>```

>[!tip] Libreria `std_logic_1164`
>Questa libreria contiene due due tipi principali. Il primo, `std_logic` assume diversi valori che rappresentano uno stato logico:
>- `'U'`: Uninitialized
>- `'X'`: Unknown
>- `'1'`
>- `'0'`
>- `'Z'`: Alta impedenza
>- `'W'`: Weak unknown
>- `'L'`: Weak `'0'`
>- `'H'`: Weak `'1'`
>- `'-'`: Indifferenza
>
>E `std_logic_vector`, che è una versione array di `std_logic`.

È inoltre possibile dichiarare dei generics, che consentono di creare entità parametriche, e entity statement, che contengono dichiarazioni comuni a tutte le architetture.
### Architetture
>[!note]
>Ad ogni entità viene associata una o più architetture. Ogni architettura rappresenta una diversa implementazione di un'entità, e la configurazione deciderà quale specifica implementazione verrà utilizzata per la simulazione o sintesi.
>
>```vhdl
>architecture ARCHITECTURE_NAME of ENTITY_NAME is
>-- header dichiarativo
>begin
>-- body
>end architecture;
>```
>
>

>[!tip] Costanti
>Le costanti, come nei linguaggi di programmazione, aiutano a tenere il codice in ordine:
>
>```vhdl
>constant NOME: type := expression; 
>```

>[!tip] Segnali
>I segnali sono l'astrazione dei "collegamenti fisici tra i componenti":
>
>```vhdl
>signal NOME: type := expression;
>```

Per istanziare un componente si usa la sintassi:
```vhdl
instance_name: component_name
	port map(port mappings)
```

### Alcuni costrutti importanti
>[!note] Operatore di concatenamento
>L'operatore di concatenamento `&` concatena in un segnale più grande.
>```vhdl
>signal low_bytes: std_logic_vector(0 to 15);
>signal high_bytes: std_logic_vector(0 to 15);
>signal overall: std_logic_vector(0 to 31);
>
>overall <= high_bytes & low_bytes;
>```

>[!note] Operatore when/else
>L'operatore `when else` ci permette di valutare condizioni.
>```vhdl
>output <= "001" when input = "100" else
>	"010" when input = "010" else
>	"100" when input = "001" else
>	"000";
>```
>
>Quando facciamo condizioni con un solo assegnamento possiamo usare `with`:
>```vhdl
>with input select
>	output <= "001" when "100",
>		"010" when "010",
>		"100" when "001",
>		"000" when others
>```

>[!note] Istruzione for
>L'istruzione `for generate` consente la creazione di componenti multipli:
>```vhdl
>test_generator: for i in 0 to 10 generate
>	test_comp : test port map (inp(i), inp(i + 1));
>end generate;
>``` 

