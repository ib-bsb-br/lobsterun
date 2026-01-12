<purpose>
  Produce a comprehensive, impersonal delivery record that describes how the
  lobsterun project should be ported to the Lobster programming language and
  refactored into ratpoison-focused .lobster scripts, while aligning the plan
  to the specified Debian-based ARM hardware profile and the referenced
  Lobster/ratpoison documentation sources.
</purpose>

<context>
  <environment>
    <hardware_profile>
      <cpu>Rockchip RK3588 with 4x Cortex-A55 and 4x Cortex-A76 cores (AArch64).</cpu>
      <memory>32535MB total system memory.</memory>
      <graphics>
        <display_resolution>2560x1944 pixels.</display_resolution>
        <display_adapter>arm Mali family; OpenGL renderer reported as llvmpipe.</display_adapter>
        <x_server>X.Org Foundation 1.20.11.</x_server>
      </graphics>
      <audio>
        <device>rockchip-es8388/rockchip-es8388i.</device>
        <device>rockchip-hdmi0.</device>
      </audio>
      <operating_system>
        <distro>Debian GNU/Linux 11.11.</distro>
        <kernel>Linux 5.10.198 (aarch64).</kernel>
        <glibc>Debian GLIBC 2.31-13+deb11u13.</glibc>
      </operating_system>
    </hardware_profile>
    <runtime_assumptions>
      <display_server>X.Org session availability is required for ratpoison.</display_server>
      <input_devices>Multiple keyboard-class input devices are available.</input_devices>
    </runtime_assumptions>
  </environment>

  <constraints>
    <constraint>All output artifacts must be expressed as Lobster source files
    (.lobster) that can orchestrate ratpoison commands and frame navigation.</constraint>
    <constraint>Key ratpoison behavior must be preserved: keyboard-driven control,
    frame-centric layout, and prefix-key binding conventions.</constraint>
    <constraint>The refactor must emphasize Lobster language traits such as static
    typing and compile-time memory management.</constraint>
    <constraint>Configuration guidance must respect Debian 11.11 and the ARM64
    execution environment, including the X.Org session version in use.</constraint>
  </constraints>

  <domain_notes>
    <note>Lobster is described as a statically typed language with Python-like
    syntax and compile-time memory management, intended to be lightweight and
    friendly while doing heavy lifting for the developer.</note>
    <note>ratpoison is a window manager that operates without mouse dependency,
    uses a prefix key (default Control-t), and manages windows in non-overlapping
    frames with maximized windows per frame.</note>
    <note>ratpoison commands can be issued via command-line invocation with
    -c/--command, which requires an active ratpoison instance on the target
    display/screen.</note>
  </domain_notes>
</context>

<variables>
  <variable name="[[task_request]]" required="true">
    <description>Port the lobsterun repository to Lobster and refactor the
    implementation into ratpoison-oriented .lobster scripts that map project
    behaviors to ratpoison window manager commands.</description>
  </variable>
  <variable name="[[source_repository]]" required="true">
    <description>https://github.com/ib-bsb-br/lobsterun</description>
  </variable>
  <variable name="[[lobster_language_source]]" required="true">
    <description>https://github.com/aardappel/lobster/ and the bundled
    documentation XML source file.</description>
  </variable>
  <variable name="[[ratpoison_sources]]" required="true">
    <description>ratpoison source archive text listing and ratpoison
    documentation markdown.</description>
  </variable>
  <variable name="[[hardware_profile]]" required="true">
    <description>Debian GNU/Linux 11.11 on Rockchip RK3588 (AArch64), with X.Org
    1.20.11 and 2560x1944 display.</description>
  </variable>
</variables>

<instructions>
  <instruction>1. Establish a Lobster-based module layout that mirrors the
  lobsterun feature set, selecting Lobster constructs compatible with static
  typing and compile-time memory management.</instruction>

  <instruction>2. Identify ratpoison control points (e.g., command-line control
  with -c, frame navigation, and key binding discovery) and map lobsterun
  behaviors to those operations.</instruction>

  <instruction>3. Convert each mapped behavior into a dedicated .lobster script
  that emits ratpoison commands for frame management, window switching, and
  key-driven workflow actions.</instruction>

  <instruction>4. Incorporate hardware-aware constraints: target Debian 11.11,
  AArch64, and an X.Org session at 2560x1944, ensuring any assumptions about
  display or input remain consistent with the hardware profile.</instruction>

  <instruction>5. Document all decisions, including inferred or hypothesized
  integration steps, and surface any discrepancies between sources as explicit
  observations.</instruction>
</instructions>

<output_format_specification>
  <format>Markdown</format>
  <requirements>
    <requirement>The document must enumerate the Lobster-to-ratpoison mapping and
    produce a catalog of .lobster scripts with their intended ratpoison command
    coverage.</requirement>
    <requirement>All ratpoison command references must preserve the described
    invocation pattern that requires a running ratpoison instance.</requirement>
    <requirement>The hardware profile must be reflected in configuration notes
    and execution assumptions.</requirement>
  </requirements>
</output_format_specification>

<examples>
  <example>
    <scenario>Command dispatch and frame navigation mapping</scenario>
    <input_data>
      <lobster_task>Generate a Lobster script that issues ratpoison commands
      through the -c flag.</lobster_task>
      <ratpoison_reference>ratpoison -c "echo hello world"</ratpoison_reference>
    </input_data>
    <output>
      A .lobster script should construct a command string that targets ratpoison
      with the -c option, ensuring ratpoison is already running for the active
      display. The script should then associate the action with the prefix-key
      workflow (Control-t) to remain consistent with the default key map.
    </output>
  </example>

  <example>
    <scenario>Frame management alignment</scenario>
    <input_data>
      <lobster_task>Expose frame state for the current screen.</lobster_task>
      <ratpoison_reference>fdump / frestore to save and restore frames.</ratpoison_reference>
    </input_data>
    <output>
      A .lobster script should serialize frame layout using the ratpoison
      fdump command and preserve it for later restoration with frestore, using
      the same frame selection semantics described in the ratpoison reference.
    </output>
  </example>
</examples>

<self_check>
  <checklist>
    <item>All template fields have been repopulated with data derived from the
    lobster, ratpoison, and hardware sources.</item>
    <item>Every described workflow is achievable via ratpoison commands that
    rely on the keyboard-driven prefix map.</item>
    <item>All Lobster guidance reflects static typing and compile-time memory
    management characteristics from the reference documentation.</item>
    <item>Hardware constraints for Debian 11.11, ARM64, and X.Org 1.20.11 are
    visible in execution assumptions.</item>
  </checklist>
</self_check>

<evaluation_notes>
  <test_cases>
    <case>Verify that ratpoison command dispatch works with a running instance
    using -c/--command on the target display.</case>
    <case>Validate that frame dump/restore scripts preserve non-overlapping
    frame layouts.</case>
    <case>Confirm Lobster scripts compile on AArch64 under Debian 11.11 with
    the documented Lobster toolchain.</case>
    <case>Ensure prefix-key bindings (Control-t) align with ratpoison defaults
    and do not assume mouse-driven actions.</case>
  </test_cases>
  <success_definition>The ported Lobster scripts provide keyboard-centric
  ratpoison automation consistent with the reference behavior and run within the
  specified hardware profile.</success_definition>
</evaluation_notes>

<documentation>
  <usage>
    <step>Review the source repository scope and extract functional modules for
    translation to Lobster equivalents.</step>
    <step>Use ratpoison documentation to select command targets for each module,
    ensuring that commands are compatible with the running ratpoison instance.</step>
    <step>Generate .lobster scripts for each mapped capability and annotate how
    they correspond to ratpoison key-driven workflows.</step>
  </usage>
  <known_limitations>
    <limitation>ratpoison command execution requires a running ratpoison window
    manager on the target display/session.</limitation>
    <limitation>Frame operations assume non-overlapping frame layouts and may
    need adjustment for custom frame selector configurations.</limitation>
    <limitation>The Lobster toolchain must be available for ARM64 to compile and
    execute the scripts on the target system.</limitation>
  </known_limitations>
</documentation>
