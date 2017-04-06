project(basic_cmds)

add_compile_options(
	-nostdinc
)

add_darling_executable(mesg mesg/mesg.c gen/mesg_vers.c)
add_darling_executable(uudecode uudecode/uudecode.c uudecode/base64.c gen/uudecode_vers.c)
add_darling_executable(uuencode uuencode/uuencode.c uuencode/base64.c gen/uuencode_vers.c)
add_darling_executable(write write/write.c gen/write_vers.c)

install(TARGETS mesg uudecode uuencode DESTINATION libexec/darling/usr/bin)

# TODO: Should have `tty` as the group
install(TARGETS write
	PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE SETGID WORLD_READ WORLD_EXECUTE
	DESTINATION libexec/darling/usr/bin)

install(FILES
	mesg/mesg.1
	uudecode/uudecode.1
	uuencode/uuencode.1
	write/write.1

	DESTINATION libexec/darling/usr/share/man/man1
)

install(FILES uuencode/uuencode.5 DESTINATION libexec/darling/usr/share/man/man5)
