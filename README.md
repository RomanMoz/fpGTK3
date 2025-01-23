# fpGTK3
GTK3 Library for Free Pascal

Example:

{$mode objfpc}
Program GtkInit;

Uses math {required}, classes, gtk3, gobject2, glib2;

Var
  window: PGtkWidget;
  drawing_area: PGtkWidget;
  err: PPGError;

Procedure on_window_destroy(theobject: PGObject; data: gpointer); cdecl;
Begin
  gtk_main_quit();
End;

Begin
  
  SetExceptionMask([exInvalidOp, exDenormalized, exZeroDivide, exOverflow, exUnderflow, exPrecision]); // required

  gtk_init(@argc, @argv);

  window := gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_window_set_title(PGtkWindow(window), 'Sample Window');
  gtk_window_set_default_size(PGtkWindow(window), 800, 600);
 
  g_signal_connect_data(window, 'destroy', TGCallback(@on_window_destroy), nil, nil, 0);

  gtk_widget_show_all(window);
  gtk_main;
End.

