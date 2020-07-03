unit Unit1;

{$mode objfpc}{$H+}

interface

uses
  Classes, SysUtils, FileUtil, LazSerial, Forms, Controls, Graphics, Dialogs,
  StdCtrls, ExtCtrls;

type

  { TForm1 }

  TForm1 = class(TForm)
    Button1: TButton;
    Button2: TButton;
    Button3: TButton;
    CheckBox1: TCheckBox;
    CheckBox2: TCheckBox;
    Edit1: TEdit;
    Edit2: TEdit;
    Edit5: TEdit;
    Label1: TLabel;
    Label2: TLabel;
    LazSerial1: TLazSerial;
    Memo1: TMemo;
    Timer1: TTimer;
    procedure Button1Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);
    procedure CheckBox1Change(Sender: TObject);
    procedure Edit1Change(Sender: TObject);
    procedure Edit3Change(Sender: TObject);
    procedure FormCreate(Sender: TObject);
    procedure LazSerial1RxData(Sender: TObject);
    procedure Timer1Timer(Sender: TObject);
  private
    { private declarations }
  public
    { public declarations }
  end;

var
  Form1: TForm1;
  ConnectButton : Boolean;
  Sending       : Boolean;
  Result        : Boolean;

implementation

{$R *.lfm}

{ TForm1 }

procedure TForm1.Edit1Change(Sender: TObject);
begin

end;

procedure TForm1.Edit3Change(Sender: TObject);
begin

end;

function IsValidEntry(s:String):Boolean;
var
  n:Integer;
begin
  Result := True;
  for n := 1 to Length(s) do begin
    if (s[n] < '0') or (s[n] > '9') then
    begin
       Result := False;
       exit;
    end;
  end;
end;

procedure TForm1.Button2Click(Sender: TObject);
begin
  if ConnectButton = False then
  begin
    LazSerial1.ShowSetupDialog;
    LazSerial1.Open;
    Memo1.Lines.Add('Port '  + LazSerial1.Device + ' is Connected');
    ConnectButton := True;
  end
  else
  begin
    Memo1.Lines.Add('Port '  + LazSerial1.Device + ' is not Connected');
    LazSerial1.Close;
    ConnectButton := False;
  end;

end;

procedure TForm1.Button3Click(Sender: TObject);
begin
  LazSerial1.WriteData(Edit1.Text);
  Memo1.Lines.Add(Edit1.Text);
  Edit5.SetFocus;
end;

procedure TForm1.CheckBox1Change(Sender: TObject);
begin
  if CheckBox1.Checked then
    Edit2.Enabled:=True
  else
    Edit2.Enabled:=False;
end;

procedure TForm1.Button1Click(Sender: TObject);
begin

  if LazSerial1.Active then
  begin

    IsValidEntry(Edit1.Text);
    if Result = False then
    begin
      Memo1.Lines.Add('Not a valid address');
      exit
    end;

    {IsValidEntry(Edit2.Text);
    if Result = False then
      exit;}

    if CheckBox1.Checked then
    begin

    end
    else
    begin
      LazSerial1.WriteData('W'+Edit1.Text);
      Memo1.Lines.Add('W '+Edit1.Text);
      LazSerial1.WriteData('D'+Edit5.Text);
      Memo1.Lines.Add('D '+Edit5.Text);
      Edit1.SetFocus;
      Button1.Enabled := False;
      Sending         := True;
    end;

  end;

end;

procedure TForm1.FormCreate(Sender: TObject);
begin
  Form1.Caption:='RS-485 Test';
  Edit1.Clear;
  Edit2.Clear;
  Edit2.Enabled:=False;
  Edit5.Clear;
  Memo1.Clear;
  Sending:=False;
  ConnectButton:=False;
end;

procedure TForm1.LazSerial1RxData(Sender: TObject);
begin
  //LazSerial
end;

procedure TForm1.Timer1Timer(Sender: TObject);
begin
  if LazSerial1.Active then
    Button2.Caption:='Disconnect'
  else
    Button2.Caption:='Connect';
end;

end.

