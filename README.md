# CANDUCCI CEP

__Web Service provided by http://viacep.com.br/__

[![Canducci Cep](https://rbofmg-sn3302.files.1drv.com/y3p8AkJ61QPgaBciQr7eYXQXiRi_7vKvXeeS_iKg4LYLtV40qPSzTgl55vh1CklI1U_9afR401m-1tKo_teUQMxFXOuZP3ZW8gRjgVWzYQaLSxFdSyrznBiv0wH5i6sI9irnoOl6Nwgv1ZES9w927pS2Q/cep.png)](https://packagist.org/packages/canducci/cep)

## Quick start

### Required setup

In the `require` key of `composer.json` file add the following

```PHP
"canducci/cep": "dev-master"
```

Run the Composer update comand

    $ composer update

In your `config/app.php` add `'Canducci\Cep\CepServiceProvider'` to the end of the `providers` array

```PHP
'providers' => array(
    ...,
    'Illuminate\Workbench\WorkbenchServiceProvider',
    'Canducci\Cep\CepServiceProvider',

),
```

At the end of `config/app.php` add `'Cep' => 'Canducci\Cep\Facade\Cep'` to the `aliases` array

```PHP
'aliases' => array(
    ...,
    'View'       => 'Illuminate\Support\Facades\View',
    'Cep'        => 'Canducci\Cep\Facade\Cep',

),
```

##How to Use

To use is very simple, pass the ZIP and calls the various types of returns, like this:

```PHP
$cep = Cep::find('01414-001');
```

Type returns:
```PHP    
$cepInfo = $cep->toJon();

$cepInfo->result();

    {
        "cep": "01414-001",
        "logradouro": "Rua Haddock Lobo",
        "bairro": "Cerqueira César",
        "localidade": "São Paulo",
        "uf": "SP",
        "ibge": "3550308"
    }
```

```PHP    
$cepInfo = $cep->toArray();

$cepInfo->result();

    Array
    (
        [cep] => 01414-001
        [logradouro] => Rua Haddock Lobo
        [bairro] => Cerqueira César
        [localidade] => São Paulo
        [uf] => SP
        [ibge] => 3550308
    )
```

```PHP    
$cepInfo = $cep->toObject();
    
$cepInfo->result();
    
    stdClass Object
    (
        [cep] => 01414-001
        [logradouro] => Rua Haddock Lobo
        [bairro] => Cerqueira César
        [localidade] => São Paulo
        [uf] => SP
        [ibge] => 3550308
    )
```

```PHP    
$cepInfo = $cep->toXml();

$cepInfo->result();
    
    <?xml version="1.0" encoding="utf-8"?>
    <xmlcep>
    	<cep>01414-001</cep>
    	<logradouro>Rua Haddock Lobo</logradouro>
    	<bairro>Cerqueira César</bairro>
    	<localidade>São Paulo</localidade>
    	<uf>SP</uf>
    	<ibge>3550308</ibge>
    </xmlcep>
```

```PHP    
$cepInfo = $cep->toSimpleXml();

$cepInfo->result();

    SimpleXMLElement Object
    (
        [cep] => 01414-001
        [logradouro] => Rua Haddock Lobo
        [bairro] => Cerqueira César
        [localidade] => São Paulo
        [uf] => SP
        [ibge] => 3550308
    )
```

```PHP    
$cepInfo = $cep->toPiped();
    
$cepInfo->result();
    
    cep:01414-001|logradouro:Rua Haddock Lobo|bairro:Cerqueira César|localidade:São Paulo|uf:SP|ibge:3550308
```
    
```PHP    
$cepInfo = $cep->toQuerty();
    
$cepInfo->result();
    
    cep=01414-001&logradouro=Rua+Haddock+Lobo&bairro=Cerqueira+C%C3%A9sar&localidade=S%C3%A3o+Paulo&uf=SP&ibge=3550308
```   
    
__To check if any errors had to do:__

```PHP

$cep = Cep::find('01414000');

$cepInfo = $cep->toSimpleXml();


if ($cepInfo->passed())
{

    return $dados->result();

}
else
{

    return 'Cep não encontrado';

}


```
