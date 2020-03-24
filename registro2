<?php
session_start();
//INCLUDE CONFIG FILE
include 'config.php';
$content = '';
$array_temp = [];
//$_SESSION[KEY] = VALUE
$html->print_pre($_SESSION);
$html->print_pre($_POST);
//QUITAR ELEMENTO DE UN ARRAY con unset($array['key']);
//$array_td = [];
//PARA REALIZAR PRUEBAS DEV.
$input_class = 'form-control mt-2';
$input_style ='width : 100px; heigth : 1px';

//DEFINIR INPUTS O BOTONES PRINCIPALES
$nombre = $utilities->post('nombre');
$apellido_p = $utilities->post('apellido_p');
$apellido_m = $utilities->post('apellido_m');
$telefono = $utilities->post('telefono');
$key_rewrite = $utilities->post('key_rewrite');
$key_delete = $utilities->post('key_delete');
//definir inputs de la TABLA
$nombre_t = $utilities->post('nombre_t');
$apellido_p_t = $utilities->post('apellido_p_t');
$apellido_m_t = $utilities->post('apellido_m_t');
$telefono_t = $utilities->post('telefono_t');

//RECUPERAR ARREGLO DE SESIÓN
if(!array_key_exists('session_values', $_SESSION))$_SESSION['session_values'] = [];

// 1) ------------------------ FORM HACER VALIDACIONES DE REGISTRO ------------------------
if(array_key_exists('nombre', $_POST)){
  if($nombre == '' || $apellido_p == '' || $apellido_m == '' || $telefono == ''){
    $html_alert = $html->alert('Mensaje', 'Revisa tu información', 'danger');
  }else{
    //AGREGAR NUEVO VALOR A SESIÓN
    $_SESSION['session_values'][] = [
      'nombre' => $nombre,
      'apellido_p' => $apellido_p,
      'apellido_m' => $apellido_m,
      'telefono' => $telefono
    ];
    //RESTEAR VALORES
    $nombre = $apellido_p = $apellido_m = $telefono = '';
    //MOSTRAR MENSAJE SATISFACTORIO
    $html_alert = $html->alert('Mensaje', 'Datos registrados', 'success');
  }
  $content .= $html->div($html_alert, ['class' => 'mt-4']);
}

// 2) ------------------------ ELIMINAR VALOR DE SESIÓN ------------------------
if(is_numeric($key_delete) && isset($_SESSION['session_values'][$key_delete])){
  $arr_valor_delete = $_SESSION['session_values'][$key_delete];
  $nombre_delete = $utilities->key('nombre', $arr_valor_delete);
  unset($_SESSION['session_values'][$key_delete]);
  $content .= $html->alert('Eliminar', "Registro número $key_delete de {$nombre_delete} eliminado", 'success');
}
// 4) ------------------------EDITAR DATOS----------------------------------------
//if(is_numeric($key_rewrite) && isset($_SESSION['session_values'][$key_rewrite])){
  if(array_key_exists('nombre_t', $_POST)){
    //crear nuevo arreglo
    $array_temp[]= [
      'nombre_t' => $nombre_t,
      'apellido_p_t' => $apellido_p_t,
      'apellido_m_t' => $apellido_m_t,
      'telefono_t' => $telefono_t
    ];

    }
    

//}
// 4) ------------------------ MOSTRAR TABLA DE ACUERDO A SESIÓN  ------------------------
$arr_session = $utilities->key('session_values', $_SESSION);

if(is_array($arr_session) && !empty($arr_session)){

  //RECORRER CICLO SE SESIÓN DE VALORES
  foreach($arr_session as $key_data => $arr_data){

    $val_nombre = $utilities->key('nombre', $arr_data);
    $val_apellido_p = $utilities->key('apellido_p', $arr_data);
    $val_apellido_m = $utilities->key('apellido_m', $arr_data);
    $val_telefono = $utilities->key('telefono', $arr_data);
    $html_input_hidden2 = $html->input(['name' => 'key_rewrite', 'value' => "$key_data", 'type' => 'hidden']);
    $html_input_hidden = $html->input(['name' => 'key_delete', 'value' => "$key_data", 'type' => 'hidden']);

    //AGREGAR NUEVO RENGLÓN DEL CICLO
    $array_td[] = [
      $input_name_tab= $html->input(['name' => 'nombre_t', 'value' => $nombre_t, 'type' => 'text', 'placeholder' => $val_nombre, 'style'=> $input_style,'class' => $input_class]),
      $input_apellido_p_tab= $html->input(['name' => 'apellido_p_t', 'value' => $apellido_p_t, 'type' => 'text', 'placeholder' => $val_apellido_p, 'style'=> $input_style,'class' => $input_class]),
      $input_apellido_m_tab= $html->input(['name' => 'apellido_m_t', 'value' => $apellido_m_t, 'type' => 'text', 'placeholder' => $val_apellido_m, 'style'=> $input_style,'class' => $input_class]),
      $input_tel_tab= $html->input(['name' => 'telefono_t', 'value' => $telefono_t, 'type' => 'text', 'placeholder' => $val_telefono, 'style'=> $input_style,'class' => $input_class]),
      $html->form($html_input_hidden2.$html->button('Guardar', ['class' => 'btn btn-danger btn-block mt-2']), ['method' => 'post']),
      $html->form($html_input_hidden.$html->button('Eliminar', ['class' => 'btn btn-danger btn-block mt-2']), ['method' => 'post'])

    ];
  }
}

//CONTENIDO PRINCIPAL
$input_nombre = $html->input(['name' => 'nombre', 'value' => $nombre, 'type' => 'text', 'placeholder' => 'Nombre', 'class' => $input_class]);
$input_apellido_p = $html->input(['name' => 'apellido_p', 'value' => $apellido_p, 'type' => 'text', 'placeholder' => 'Apellido P.', 'class' => $input_class]);
$input_apellido_m = $html->input(['name' => 'apellido_m', 'value' => $apellido_m, 'type' => 'text', 'placeholder' => 'Apellido M.', 'class' => $input_class]);
$input_telefono = $html->input(['name' => 'telefono', 'value' => $telefono, 'type' => 'text', 'placeholder' => 'Teléfono', 'class' => $input_class]);

//BUTTON - HTML
$btn_registrar = $html->button('Registrar', ['class' => 'btn btn-primary btn-block mt-4']);

//CREAR TABLA HTML
if(empty($array_td))$html_table = '';
else{
  $array_table = [];
  $array_table['attr'] = ['class' => 'table table-striped table-dark mt-3'];
  $array_table['th'][] = ['Nombre', 'Ap.Paterno', 'Ap.Materno', 'Teléfono', ''];
  $array_table['td'] = $array_td;
  $html_table = $html->table($array_table);
}

//CREAR RENGLONES
$html_row_principal = $html->row([
  ['html' => $input_nombre, 'col' => 12, 'sm' => 6, 'md' => 6, 'lg' => 3, 'xl' => 3],
  ['html' => $input_apellido_p, 'col' => 12, 'sm' => 6, 'md' => 6, 'lg' => 3, 'xl' => 3],
  ['html' => $input_apellido_m, 'col' => 12, 'sm' => 6, 'md' => 6, 'lg' => 3, 'xl' => 3],
  ['html' => $input_telefono, 'col' => 12, 'sm' => 6, 'md' => 6, 'lg' => 3, 'xl' => 3],
  ['html' => '', 'col' => 12, 'sm' => 12, 'md' => 6, 'lg' => 6, 'xl' => 6],
  ['html' => $btn_registrar, 'col' => 12, 'sm' => 12, 'md' => 6, 'lg' => 6, 'xl' => 6],
]);
$content .= $html->form($html_row_principal, ['method' => 'post']);

//HTML DE TABLA A MOSTRAR
$content .=  $html->row([
  ['html' => $html_table, 'col' => 12]
]);

//ECHO TEMPLATE
echo $html->template(TEMPLATE_JSON, [
  'html' => $content,
  'class' => 'ml-3 mr-3'
]);
